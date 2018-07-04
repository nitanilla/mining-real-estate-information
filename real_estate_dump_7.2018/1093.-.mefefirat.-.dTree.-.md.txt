# jQuery Tree Menu

A tree menu plugin for jQuery framework

[![GitHub version](https://d25lcipzij17d.cloudfront.net/badge.svg?id=gh&type=5&v=1.0)](https://github.com/mefefirat/dTree)

## Examples

http://jsfiddle.net/nnLg07ag/10/

<a href="http://jsfiddle.net/nnLg07ag/10/">![Example](http://oi61.tinypic.com/282m8ao.jpg "Example")</a>



### HTML

```html
<div class="dTree">
	<ul>
		<li><a href="#">Site</a></li>
		<li><a href="#">About the Web Site</a></li>
		<li><a href="#">Contact Us</a></li>
		<li><a href="#">Cars</a>
			<ul>
				<li><a href="#">Add New Brand</a></li>
				<li><a href="#">List All Brand</a></li>
				<li><a href="#">Mercedes - Benz</a>
					<ul>
						<li><a href="#">About the Mercedes - Benz</a></li>
						<li><a href="#">History</a></li>
						<li><a href="#">Series</a>
							<ul>
								<li><a href="#">A Series</a>
									<ul>
										<li><a href="#">A 140</a></li>
										<li><a href="#">A 150</a></li>
										<li><a href="#">A 180 CDI</a></li>
										<li><a href="#">A 200 CDI</a></li>
									</ul>
								</li>
								<li><a href="#">B Series</a>
									<ul>
										<li><a href="#">B 140</a></li>
										<li><a href="#">B 150</a></li>
										<li><a href="#">B 180 CDI</a></li>
										<li><a href="#">B Special Series</a>
											<ul>
												<li><a href="#">B Extreme</a></li>
												<li><a href="#">B Jumper</a></li>
												<li><a href="#">B Raiden</a></li>
												<li><a href="#">B Subzero</a></li>
											</ul>
										</li>
									</ul>
								</li>
								<li><a href="#">Concept Cars</a></li>
								<li><a href="#">Best Prototypes</a></li>
								<li><a href="#">List all other categories</a></li>
							</ul>
						</li>
						<li><a href="#">Custom Series</a></li>
						<li><a href="#">A+ Series for children</a></li>
						<li><a href="#">B+ Series for women</a></li>
					</ul>
				</li>
				<li><a href="#">Chevrolet</a></li>
				<li><a href="#">Saab Custom models</a></li>
				<li><a href="#">Fiat</a>
					<ul>
						<li><a href="#">Kartal SLX</a></li>
						<li><a href="#">Dogan 1.6 Turbo</a></li>
						<li><a href="#">Sahin</a></li>
						<li class="active"><a href="#">Dogan Gorunumlu Sahin</a>
							<ul>
								<li><a href="#">1.3 Motor</a></li>
								<li><a href="#">1.6 Motor</a></li>
								<li><a href="#">1.8 Motor</a></li>
								<li><a href="#">2.0 Motor</a></li>
							</ul>
						</li>
						<li><a href="#">Serce</a></li>
						<li><a href="#">Murat 131</a></li>
					</ul>
				</li>
			</ul>
		</li>
		<li><a href="#">Electronic Models</a></li>
		<li><a href="#">Real Estate</a></li>
		<li><a href="#">Bruce Lee</a></li>
		<li><a href="#">Graphics</a></li>
		<li><a href="#">Smart Phones</a>
			<ul>
				<li><a href="#">Apple</a></li>
				<li><a href="#">Samsung</a></li>
				<li><a href="#">LG</a></li>
				<li><a href="#">Sony</a></li>
				<li><a href="#">HTC</a></li>
				<li><a href="#">Samsung</a></li>
				<li><a href="#">Samsung</a></li>
				<li><a href="#">Other Models</a>
					<ul>
						<li><a href="#">First other model</a></li>
						<li><a href="#">Second other model</a></li>
					</ul>
				</li>
				<li><a href="#">Add New Model</a></li>
			</ul>
		</li>
	</ul>
</div>
```
### Call the plugin

```html
$(document).ready(function(){
	$(".dTree").dTree();
});  
```
