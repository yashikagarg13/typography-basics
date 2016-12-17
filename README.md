Application describing different challenges of attaining good typography and their solution

* **Different font sizes for different screen sizes**

   When we move from large desktops to medium screens or tablets or mobile screen which in themselves have a large range of screen sizes, we want our content to adjust and stay readable.  

   To achieve this we can make use of media queries in our CSS files. Adjust font size for different headings and paragraphs to look pretty on screen size. But there are hundred of screen sizes and its entirely impossible to make adjustments for each those. 

  CSS world has frameworks like bootstrap and gaining knowledge from them, we can try to find solution to our problem - Breakpoints! Here are some commonly use breakpoints: 

	```
	xs - 480 px - Small screen phones
	sm - 768 px - Tablets and phones
	md - 992 px - Desktop
	lg - 1200 px - Wide Desktop
	```

* **Attaining Vertical Rhythm**

	Firstly, I would like to put some light on what vertical rhythm is. It is a phenomenon of keeping consistent vertical spaces between different elements on page. Vertical rhythm help us establish hierarchy on page and convey the relation how different content is connected to each other. It gives avery professional look to our page. 

	To achieve vertical rhythm, we need a base line-height value and compute all our vertical spaces, margins, paddings, line-heights, as a multiple of that bas line height. 

	To figure out our base line-height, we need to find the value of a vertical space which gets repeated most on our page. For instance, what is the most common margin or line-height or padding we are using in our page. This value would be our base line-height. 

	We will be repeating this value on our page to bring consistency and this repetition has to vary. We definitely don't want each of our vertical space to be same. We need to be variable in order to establish hierarchy and relation between different elements of page. For achieving this variation we will use multiples of our base line height. We can do preprocess either using LESS or SASS. 

	```less
	@base-line-height: 24px;

	p { 
		line-height:  @base-line-height;
		margin-bottom: @base-line-height;
	}
	h2 {
		line-height:  @base-line-height * 2; 
		margin-bottom: @base-line-height * 2;
	}
	h4 {
		line-height:  @base-line-height * 1.5;
		margin-bottom: @base-line-height * 1;
	}
	```

* **Update typography through out the site**

	Sometimes you decide for your website a typography in terms of font-size for headings and paragraphs, vertical spaces and so on, and you grow your website on that. But a later stage you found that something is missing and its not fitting the way you presumed. Now you want to change it all through! 

	Wait a minute! Change typography throughout the site, that's a large amount of work and tedious. Changing each and every page, each and every element throughout site. But its important you see. You need your work to match your expectation. 

	Lets try to think a solution for this. What if a set base font size for our application and manipulate all other font-sizes and vertical spaces based on that. Now if we think of changing typography to lets say a bigger font-size or a smaller one, adjust vertical spaces, then all we need to do is to change our base font size and tweak our manipulations around it to handle this scenario.

	```less
	@base-font-size: 15px;
	@base-line-height: 1.6; // Unit less value
	@computed-line-height: ceil(@base-font-size * @base-line-height);

	p { 
		font-size: @base-font-size;
		line-height:  @base-line-height;
		margin-bottom: @base-line-height;
	}
	h2 {
		font-size: ceil(@base-font-size * 2.15); // 32px
		line-height:  @base-line-height * 2; // 48px
		margin-bottom: @base-line-height * 2; // 48px
	}
	h4 {
		font-size: ceil(@base-font-size * 1.6); // 24px
		line-height:  @base-line-height * 1.5; // 26px
		margin-bottom: @base-line-height * 1; // 24px
	}
	```

	Now I want to make things look bigger and all I need to tweak is following:

	```less
	@base-font-size: 20px;
	@base-line-height: 1.2; // Unit less value
	@computed-line-height: ceil(@base-font-size * @base-line-height);
	p { 
		font-size: @base-font-size;
		line-height:  @base-line-height;
		margin-bottom: @base-line-height;
	}
	h2 {
		font-size: ceil(@base-font-size * 1.8); // 36px
		line-height:  @base-line-height * 2; // 48px
		margin-bottom: @base-line-height * 2; // 48px
	}
	h4 {
		font-size: ceil(@base-font-size * 1.4); // 28px
		line-height:  @base-line-height * 1.5; // 26px
		margin-bottom: @base-line-height * 1; // 24px
	}
	```

	And I am all set!

* **Responsive Designs**

	I know you have stick too long and I swear this is the last challenge. We have read above that we need different font-sizes for different screens. Along with that we need our pages to be responsive, to be fluid as we move from different ranges of devices. We need our vertical spaces and paddings to fit in every scenario. 

	Thinking about this, we have everything we need to beat this up. We will use media queries, we will make computations on base-font and we will use our scalable unit. 

	Remember, we talked about them just a few minutes before - Em and Rem.  

	Lets use rem and we know it is relative base font size of root element. If we adjust the font size for our root element for different screens using media queries and make all are manipulations in terms of rem, we are all set :). Let see

	```less
	html {
		font-size: 16px;
	}
	@media (max-width: 480px) {
		html {
			font-size: 16px;
		}
	}
	@media (min-width: 480px) and (max-width: 1200px) {
		html {
			font-size: 18px;
		}
	}

	@media (min-width: 1200px)  {
		html {
			font-size: 20px;
		}
	}

	@line-height: 1.5rem;

	.container {
		max-width: 32rem; // 75 chars per line.
		margin: 0 auto;
		padding: @line-height * 2;
		@media (max-width: 480px) { // smaller screen
			padding: @line-height * 0.8;
		}
	}

	h2 {
		font-size: 2.25rem;
		line-height: @line-height * 2;
		margin: 0 0 @line-height * 2 0;
	}
	```

	In above example, we set different font size for html tag under different break points and all our computations are rem based. So now the line-heights, margins will differ for different screens based on the base font size our root element html will have. Thus, we achieved responsive layout.
