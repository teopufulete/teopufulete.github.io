---
title: The beginnings of dinobot
author: Teo
layout: post
---
<header> <h3> Challenges of browser emulation with Selenium in Java </h3> </header>
<p> I got inspired to start this project after seeing a Youtube <a href="https://www.youtube.com/watch?v=Du__JfXqsAs">video</a> about android game app automatization in Python. I decided to turn the difficulty up a knotch and attempt my first ever project in Java: a bot that plays the Google Chrome offline dinosaur game. This is how <a href="https://github.com/teopufulete/dinobot">dinobot</a> was born, and I'm very thrilled to see where it will lead, as I have many improvements in mind, but that's for another <a href="">post</a>. Now let's dive in! </p>

<h3>Setting up: Creating a Maven project in Eclipse for the first time</h3>
<p> Right of the bat I faced the difficulties, but nothing a few minutes (<sub> or hours </sub>) of googling couldn't solve. I learned how to set up a Maven project in Eclipse and with all the required dependencies for the Selenium imports I wanted using this <a href="https://www.techbeamers.com/create-selenium-webdriver-maven-project/">tutorial</a>. </p>

<h3>Broswer Emulation</h3>
<p> Needing to emulate Chrome I had to download the Selenium Chrome <a href="
https://chromedriver.chromium.org/downloads">driver</a> compatible with my current Chrome version. One of the first bugs I ran into was initializing the driver- inputing the its path did not seem to work, so I just ended up moving the executable into the dinobot project directory. The following code excerpt initializes the driver and starts up the bot. </p>
{% highlight java linenos %}public class GameStart {
	public static void main(String[] args) {
        //initialize driver
        System.setProperty("webdriver.chrome.driver", "chromedriver.exe");
        //start dinobot
        new TRexBot().startGame();
    }
}{% endhighlight %}

<p> The next code excerpt is from the main TRexBot class, that opens a new Chrome window and browses to the game's link.
{% highlight java linenos %}public class TRexBot {
  //class level variables 
	private ChromeDriver driver;
	private WebElement window;
    public TRexBot() {
    }
    // initialize a new chrome instance
    private void initializeDriver() {
    	driver =  new ChromeDriver();
    }
    private void initializeGamePage() {
      // go to the chrome dino game page
      driver.get("chrome://dino/");
      // find the element we need to analyze
      window = driver.findElement(By.cssSelector(".runner-canvas"));
      new WebDriverWait(driver, 1000).until(ExpectedConditions.visibilityOf(window));
	//add delay to for page be loaded before starting the game 
       checkPageIsReady(1000);
    }
    public void startGame() {
        initializeGamePage();
        // the start game function will be discussed later
        start();
    }
    {% endhighlight %}</p>

<p><span class="image left"><img src="{{'assets/images/dino.png' | relative_url }}" alt="" /></span>What I struggled with the most was line 15 from above: figuring out how to find the webpage element which reresented the container of the game itself. I inspected different parts of the page using Chrome Dev Tools and eventually found what I was looking for. I was only able to use the game canvas after a lengthy dive into the specific <a href="
https://www.selenium.dev/documentation/en/getting_started_with_webdriver/locating_elements/">documentation</a>. I cannot stress how usefull reading the docs is and how all of us need to do more of it. </p>
<p></p>
<p></p>

<h3>Algorithm implementation</h3>
<p> The game has very simple rules: dodge the incoming static (cactuses on the ground) or moving (bird) obstacles. The velocity of the dino increases as the game progresses, which would normally complicate things, but in our case it should not be a problem as we directly inject the webpage js script into our code to get the dino's current speed. This is the general JavascriptExecutor object: 

{% highlight java linenos %}private Object executeScript(String command) {
		return ((JavascriptExecutor)driver).executeScript(command);
		}{% endhighlight %}</p>

<p> Now let's see it in action! Using the java.util.Map as well as <b>executescript</b> I created an object that takes each one of the incoming obstacles visible in the horizon and maps it to their position on the oX axis. The position of the dino on the x axis, as well as it's current speed are also readily available upon returning more javascript code.
{% highlight java linenos %}private Boolean isObstaclePresent() {
        Map<String, Long> obstacle = (Map<String, Long>) executeScript("return Runner.instance_.horizon.obstacles.filter(o => (o.xPos > 25))[0] || {}");
        Long tRexPos = (Long) executeScript("return Runner.instance_.tRex.xPos");
        Double currentSpeed = (Double) executeScript("return Runner.instance_.currentSpeed");
	{% endhighlight %}</p>
	
<p> Determining when to jump over an obstacle depends on the current speed of the dino and the distance from the dino to the obstacle. The default parameter was set to private static final int DEFAULT_DISTANCE = 0.
{% highlight java linenos %}Long distanceToStartJump = firstJump ? new Long(DEFAULT_DISTANCE + 180) : new Long(DEFAULT_DISTANCE + 100);
        //dynamically calculate the distance difference to 
        if(currentSpeed >= 10) {
            distanceToStartJump = Math.round(distanceToStartJump + (20 * (currentSpeed % 10))) + 40;
        }
        //speed is > 13, space bar needs to be pressed in advance
        if(currentSpeed > 13) {
            distanceToStartJump += 50;
        }{% endhighlight %}</p>

<p> Of course, there is no point in jumping if there is no obstacle so we check for one based on 2 conditions: the object obstacle cannot be empt and needs to have a position on the x axis. We check for this using the <a href="https://www.baeldung.com/java-map-key-from-value">getKey method</a>. If these 2 conditions are met, we calculate the <b>currentDistanceToObstacle</b> by subtracting the dino's position on the oX axis from the obstacles position. Now, if the dino is in the appropriate position to jump (line #) it will perform the action.
 {% highlight java linenos %}         // Check if obstacle is present 
        if (obstacle != null && obstacle.containsKey("xPos")) {
        	//If obstacle is flying, jump only if dino height >= vertical position of the obstacle 
       	 	if (obstacle.get("width") == FLYING_OBSTACLE_WIDTH && obstacle.get("yPos") < TREX_HEIGHT) {
       	 		return false;
       	 	}
       	 	Long currentDistanceToObstacle = obstacle.get("xPos") - tRexPos;
        	       	 	if (obstacle.get("xPos") > tRexPos && currentDistanceToObstacle <= distanceToStartJump) {
       	 		if (firstJump) {
       	 			firstJump = false;
       	 		}
       	 		System.out.println("Identified Obstacle at "+ currentDistanceToObstacle);
       	 		return true;
       	 	}
        }{% endhighlight %} </p>

<p> But how do we get the dino to jump in the first place. We use selenium's <b>sendKeys</b> method to input space.
{% highlight java linenos %}    private void jump() {
    	new Actions(driver).sendKeys(window, Keys.SPACE). build().perform();
    }{% endhighlight %} </p>

<p> One problem to be aware of is that the bot might start 'playing' before the webpage has loaded. To combat that, I added a ```sleep``` fuction that delays the start of the page until the page is fully loaded:
{% highlight java linenos %}     private void checkPageIsReady(Integer time) {
        try {
            Thread.sleep(time);
        } catch (Exception e) {}
    } {% endhighlight %} </p>
	
<p> Now that we have the algorithm figured out,	to start the game, the bot inputs space once than continues to jump if the obstacles are present. To avoid the while loop ordeal™ (we don't want the game to restart infinitely), I added an initial condition: the dino will only to dodge the obstacles as only until it loses.
{% highlight java linenos %}private void start() {
    	firstJump = true;
        jump();
        while (!isGameEnded()) {
        	if (isObstaclePresent()) {
        		jump();
        	}
        }
        System.out.println("Your score is:" + getScore());
    }{% endhighlight %} </p>
  
 <p> All of the code is available on <a href="https://github.com/teopufulete/dinobot">github</a>. Keep learning and happy botting💖! </p>
	
