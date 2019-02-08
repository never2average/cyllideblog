---
layout: post
title:  "Portfolios with Python <br> #2: Choosing Stocks"
date:   2018-07-30
excerpt: "Correlation, in the finance and investment industries, is a statistic that measures the degree to which two securities move in relation to each other."
image: "/images/py_portfolio2/investors-02.png"
author: Priyesh Srivastava
comments: true
---

<p>
	This is our second post on the series "Portfolios with Python" which will consist of a total of six posts that will be released weekly. In, today’s post we will attend to the second most important issue while building a portfolio,<strong>"How to go about picking stocks for our portfolio?"</strong>
</p>

<p>
	Before we answer that question, we need to answer 3 more questions first:
	<ul>
		<li><strong>What sorts of risk does our portfolio face?</strong></li>
		<p>
			First, let me define what risk actually is. Risk is the uncertainity in the calulated future return of any asset that we own. In mathematical terms, it is defined as the standard deviation of returns. Every portfolio comes with 2 types of risk:
			<ol>
				<li>Non-Systematic Risk:</li>
				<p>
					This type of risk refers to the uncertainty inherent in a company or industry investment. Examples include a change in management, a product recall, a regulatory change that could drive down company sales and a new competitor in the marketplace with the potential to take away market share from a company in which you’re invested.
				</p>
				<li>Systematic Risk:</li>
				<p>
					The risk affects the overall market – not just a particular stock or industry. This type of risk is both unpredictable and impossible to avoid completely. Examples include interest rate changes, inflation, recessions and wars.
				</p>
			</ol>
		</p>
		<li><strong>How many stocks would we need to pick?</strong></li>
		<p>
			As you would have already understood from the previous article that we need to pick stock in order to reduce risk. Now whatever we do, we cannot avoid Systematic Risk. That will be inherent with every investment you make. But we can reduce non-systematic risk by increasing the number of stocks in our portfolio as illustrated by the figure below.
			<figure>
				<img src="/images/py_portfolio2/div_risk.jpg">
			</figure>
			So, the answer to this question is that enough stocks to reduce the non-systematic risk. In my opinion, 10 to 20 stocks is more than enough. But you can even go all out and trade the entire market.
		</p>
		<li><strong>What maximum percentage of our portfolio, must we give to each stock?</strong></li>
		<p>
			This answer also, like the previous one varies widely based on your preference but mainly on your trading strategy and on how many stocks you trade. Various trading strategies have different limits on weightage but the most robust strategies that trade the entire market will normally place a maximum weight of 10% .
		</p>
	</ul>
</p>

<p>
	Now, we will answer our main question. How to pick stocks and why to pick them? Let us answer the why first and the how will become clearer.
</p>

<p>
	<h3>Approach 1:</h3>From the questions above, it is clear that the main reason for picking multiple stocks for our portfolio is to reduce the non-systematic risk. Since non-systematic risk applies to a single company/industry, you might think that all we need to do is group all the public companies into various baskets by their industry. Then see un-correlated industries and choose your favourite stocks from each basket. Now this is a pretty good approach but is discretionary and time consuming.
	<br>
	<strong>Example:</strong> You grouped all stocks trading on the National Stock Exchange by category and then decided that tobacco, aluminium, watch making, financial services and copper production are un-correlated. So you choose Vedanta, Hindalco, Titan, ITC and Bajaj Financial Services as your portfolio. Now this decision was based on my discretion and is not reproducible i.e. someone might say aluminium and copper production are related and so on.  
</p>

<p>
	<h3>Approach 2:</h3>If someone finds the first approach as time-consuming and has a more long term mindset. They may decide to trade all stocks in the stock market itself. This approach has one straightforward benefit, which is that it completely eliminates the non-systematic risk as this portfolio is as diverse as it gets. The problem is that finding a low-risk trading strategy that involves the market as a whole to make consistent profits is difficult. But if any strategy is created, it will be very robust.
	<br>
	<strong>Example:</strong>
	We may decide to invest in all of the stocks traded on the National Stock Exchange and assign weights proportional to their market cap (stock price * no. of shares traded). Now our portfolio will move by the exact same amount as the market and therefore only has systematic risk. But this strategy will only allow us to keep pace with the market not beat it. (For that there needs to be a different allocation strategy)
</p>

<p>
	<h3>Approach 3:</h3>For a good approach, we will need to use some mathematics with approach 1 and approach 2 to create a more scientific approach. We will have to use some mathematical parameter ( obviously, this is quant finance). So we will create a correlation table between various companies of the National Stock Exchange. We can use another parameter too, but I find <a href="https://en.wikipedia.org/wiki/Pearson_correlation_coefficient">Pearson's Correlation Coefficient</a> more convenient to calculate. If you don't know what that is, I will explain it in a moment.
</p>

<p>
	<h3>Pearson's Correlation Coefficient</h3>
	<p>
		Correlation coefficients are used in statistics to measure how strong a relationship is between two variables, which is stock returns in this case.
	</p>
	<p>
		Let X represent return of stock A and Y represent returns of stock B. Then the Pearson's Correlation Coefficient (r) between the 2 is defined as follows:
	</p>
	<figure class="figure" style="max-width: 300px">
	<img src="{{ "/images/py_portfolio2/pcc_formula.jpg" | absolute_url }}" alt="" style="max-width:100%;"/>
	</figure>
	<p>
		This formula will return a value between -1 and 1.
		<ul>
			<li>
				A correlation coefficient of 1 means that for every positive increase in price of Stock A, the price of Stock B tends to increase almost always.
			</li>
			<li>
				A correlation coefficient of -1 means that for every positive increase in price of Stock A, the price of stock B tends to decrease almost always.
			</li>
			<li>
				Zero means that for every increase in price of Stock A, there isn’t no significant positive or negative increase in the price of stock B.
			</li>
		</ul>
	</p>
	
</p>


<figure class="figure" style="max-width: 1000px">
<img src="{{ "/images/py_portfolio2/company_correlation_table.jpg" | absolute_url }}" alt="" style="max-width:100%;"/>
</figure>

<p>
	Using approach 3, we have made a correlation table of the various companies in the Nifty50 Index and plotted it as a heatmap. However, we have not choosen any specific stocks as such yet. And we will not until the third post. Because though the correlation table is an invaluable tool when it comes to picking stocks. Your trading strategy is the one which tells you how what to buy and how much of it to buy . The table tells you about how the various stocks in your chosen sub-universe are inter-related.
</p>

<p>
	<strong>Example:</strong>
</p>

<div style="background: #111111; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #fb660a; font-weight: bold">def</span> <span style="color: #ff0086; font-weight: bold">visualize_data</span><span style="color: #ffffff">():</span>
    <span style="color: #ffffff">df</span> <span style="color: #ffffff">=pd.read_csv(os.getcwd()+</span><span style="color: #0086d2">&#39;/data/nifty50MergedCloses.csv&#39;</span><span style="color: #ffffff">)</span>
    <span style="color: #ffffff">df[</span><span style="color: #0086d2">&quot;Date&quot;</span><span style="color: #ffffff">]=pd.to_datetime(df[</span><span style="color: #0086d2">&quot;Date&quot;</span><span style="color: #ffffff">])</span>
    <span style="color: #ffffff">df.set_index(</span><span style="color: #0086d2">&quot;Date&quot;</span><span style="color: #ffffff">,inplace=True)</span>
    <span style="color: #fb660a; font-weight: bold">print</span><span style="color: #ffffff">(df.head())</span>        
    <span style="color: #ffffff">df_corr</span> <span style="color: #ffffff">=</span> <span style="color: #ffffff">df.corr()</span>
    <span style="color: #fb660a; font-weight: bold">print</span><span style="color: #ffffff">(df_corr.head())</span>
    <span style="color: #ffffff">df_corr.to_csv(</span><span style="color: #0086d2">&#39;nifty50corr.csv&#39;</span><span style="color: #ffffff">)</span>
</pre>
</div>
<br>
<h2><u><a href="/blog/Portfolios-with-Python-1/">Previous Article</a></u></h2>
<small><strong>Advisory: Everything that will be mentioned in this series is for educational purpose only and is not financial advice. StrayLogic cannot be held accountable for any losses incurred.</strong></small>