---
layout: post
title:  "Portfolios with Python <br> #1: Introduction"
date:   2018-07-23
excerpt: "An investment portfolio can be thought of as a pie that is divided into pieces of varying sizes, representing a variety of investments to accomplish an appropriate risk-return portfolio allocation."
image: "/images/py_portfolio1/investors-01.png"
author: Priyesh Srivastava
comments: true
---

<p>
	This is our first post on the series "Portfolios with Python" which will consist of a total of six posts that will be released weekly. I will not go deep into coding in this post itself. Rather, today’s post will help us initialize and formalize a few things and allow me to get everyone onto a common starting point so that the series can go along smoothly. 
</p>

<p>Our workflow for this series will be as follows:
	<ul>
		<li><a href="#">Setup working environment and introduce a few financial concepts</a></li>
		<li><a href="/blog/Portfolios-with-Python-2/">Picking stocks for our portfolio</a></li>
		<li><a href="/blog/Portfolios-with-Python-3/">Choosing a trading strategy</a></li>
		<li><a href="/blog/Portfolios-with-Python-4/">Building a portfolio and analysing various performance metrics</a></li>
		<li><a href="/blog/Portfolios-with-Python-5/">Deeper analysis of our portfolio using more advanced metrics and thereby optimizing our portfolio</a></li>
		<li><a href="/blog/Portfolios-with-Python-6/">Visiting advanced libraries such as bt, ffn, zipline and so on</a></li>
	</ul>
</p>


<p>
	<h3>The aim of today's post is:</h3>
	<ul>
		<li>Introduce some basic financial and programming concepts</li>
		<li>Getting ready to work</li>
		<li>To familiarize you with handling financial data using <a href="https://www.quandl.com/">Quandl</a></li>
	</ul>
</p>

<p>
	Most of you who do not come from a financial background might be left wondering, <strong>Why is this guy using the word "portfolio" a hundred times? What is it and why do we even need it? </strong>
</p>

<p>
	In simple terms, a portfolio is a list of assets where you have decided to invest your money. For example, if I decide to buy 100 shares of Reliance Industries Limited, 100 shares of Titan and 100 shares of HINDALCO. Then that will become my portfolio.
</p>

<p>
	The need for a portfolio arises from the fact that we need to reduce our dependency on any one particular company so that our investment is more robust. Let me show you how. Suppose,there are 2 people: Priyesh and Shashwat.
</p>

<p>
	Priyesh spends all his money on buying shares of Reliance and Shashwat builds his portfolio like in the above example. Now who do you think will suffer greater losses if the price of Reliance shares drops. It will be Priyesh. So Shashwat has avoided losses by building a portfolio or in financial terms "Diversified his investments". Therefore if some stocks in the portfolio do badly, others will do well and therefore the net result will still be positive.
</p>

<p>
	Now I hope that everyone has understood the reason why we need a portfolio and why investing in a single stock is risky and is not normally advisable.
</p>

<p>
	Let me clarify what Quandl is and why we will be using it. Quandl is a platform for financial, economic and alternative data that serves investment professionals. Quandl sources data from over 500 publishers and cleans it for us and saves it in the very convenient csv format. We will use it because all of Quandl's data is accessible via an API.This makes information retrieval very easy and allow us to focus our attention on what is important for this series and not spend hours and hours on data collection and cleaning. The only requirement to use Quandl is an account on their website.
</p>
<p>
	In this post as well as the entirety of the 'Portfolios with Python' series, we will be using the freely available <a href="https://www.quandl.com/data/NSE-National-Stock-Exchange-of-India">Quandl NSE dataset</a> contains intraday prices of all stocks traded on NSE.
</p>

<h3>SETTING UP A WORKING ENVIRONMENT:</h3>
<p>
	In 5 simple steps, you are ready to go:
	<ol>
		<li>Signup for an account on <a href="https://www.quandl.com/">Quandl</a> and retrieve your API key. Protect this API key with your life as this is <strong>very important.</strong> It allows Quandl servers to recognize your identity and keep bots out.</li>
		<li>Install Anaconda with Python 3.6.3 or above. If it is successfully installed, then skip through steps 3 and 4</li>
		<li>If, you want to work with standard python3 distributions from MAC OS X or linux. Open up a terminal and type the following commands:
			<ul>
				<li>pip3 install numpy</li>
				<li>pip3 install pandas</li>
				<li>pip3 install matplotlib</li>
				<li>pip3 install quandl</li>
				<li>Open up Python IDLE</li>
			</ul>
		</li>
		<li>If, you want to use standard python3 distributions from Windows. Open up command prompt and type:
			<ul>
				<li>cd "path to python directory on your pc"</li>
				<li>cd Scripts</li>
				<li>pip install numpy</li>
				<li>pip install pandas</li>
				<li>pip install matplotlib</li>
				<li>pip install quandl</li>
				<li>Open up Python IDLE</li>
			</ul>
		</li>
		<li>Windows users, open up anaconda prompt (MAC OS X or Linux users open up terminal) and type spyder(or jupyter notebook, as you wish) and hit enter.</li>
	</ol>
</p>


<h3>Let the Programming Begin</h3>
<p>
	First we will add our API key to a config.py file as shown here so that we may be able to retrieve data.The advantage of using this method is that now you can open source this project on Github with no problems at all (just add config.py to .gitignore) as anyone can use your project by creating their own config.py file with the variable key and setting its value with their API key.
	<script src="https://gist.github.com/never2average/9da28bac76ffec595e5695bc53a4b3a7.js"></script>
</p>


<p>
	Quandl transfers data to your local machine over the internet. But having to call it repeatedly (while testing and learning to try out all permutations) will slow down both your program and their servers. So, we will setup the data as local csv files to speed up programs. However, you can take off on your own and continue using the quandl dataframes directly in your programs.
</p>
<p>
	How the Quandl library works in python is that, it allows us to call a get function that takes as arguements, the ticker symbol of the stock and the start and end date within which you want the data. But before, you do any of that you need to set quandl.ApiConfig.api_key as your API key that you recieved. Otherwise, you will get an error saying KeyNotSetError.
</p>

<p>
	Let us now write a function to be able to download data and save to a csv file between any start and end date.Being the "good developers" we are default arguements and error handling is a must. To avoid mess in the project directory we should save everything to /data subdirectory like the code below illustrates.  
</p>

<script src="https://gist.github.com/never2average/9e29ecaef1454528010e966bad418786.js"></script>
<p>
	This looks nice enough but what about handling one off cases like the fact that the /data subdirectory does not exist at all or the fact that we should be able to perform the same for a list of ticker symbols. Also, as a value-edition we need to store figures and dataframes in such a way that they are easily viewable.
</p>
<p>
	In short, we need to convert the above written code into something that can be put into production. So the csvRetrieve function gets converted into the setupEnvironment class in the code below that even allows us to use various features such as private access. Lines 33 through 35 allow us to be able to use this script in other files without needing to write any extras. Just calling <strong>import dataSetup</strong> will execute all the functions.
</p>

<script src="https://gist.github.com/never2average/55bffb05a005a75b4df9993ea5a2cb6e.js"></script>

<p>
	So, with that we have come to the end of this article. Where, we have setup our working environment, retrieved and stored data from Quandl and understood some good programming practices like error handling, OOP concepts and much more.
</p>

<p>
	Hope, that this was worth your time.
</p>

<p>
<h4>Assumptions:</h4>
	For this series, I assume, you have done some basic programming with python and also know how to use <strong>pandas,numpy and matplotlib.</strong> If not <a href="https://www.youtube.com/watch?v=yzIMircGU5I&list=PL5-da3qGB5ICCsgW1MxlZ0Hq8LL5U3u9y" class="blinking">click here</a> to watch some tutorials on the same.
</p>

<h2><u><a href="/blog/Portfolios-with-Python-2/">Next Article</a></u></h2>

<br>
<small><strong>Advisory: Everything that will be mentioned in this series is for educational purpose only and is not financial advice. StrayLogic cannot be held accountable for any losses incurred.</strong></small>
<br>