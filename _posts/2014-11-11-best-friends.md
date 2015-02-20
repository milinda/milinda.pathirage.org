---
layout: photos
title: Best Friends
---

<style>
h1{
		font-size: 6em;
    font-family: 'Concert One', cursive;
		color: rgba(255, 255, 255, 0.8);
    font-weight: 700;
    text-align: center;
    text-transform: uppercase;
    text-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
	}

/* Backgrounds will cover all the section
	* --------------------------------------- */
	#section0,
	#section1,
	#section2,
	#section3,
  #section4{
		background-size: cover;
	}

	/* Defining each sectino background and styles
	* --------------------------------------- */
	#section0{
		background-image: url(/img/at-hannahs-place/1.jpg);
		padding: 30% 0 0 0;
	}

  #section0 h1{
    position: absolute; bottom: 0; right: 50px;
  }

	#section2{
		background-image: url(/img/at-hannahs-place/2.jpg);
		padding: 6% 0 0 0;
	}

  #section2 h1{
    position: absolute; bottom: 0; left: 50px;
  }

	#section3{
		background-image: url(/img/at-hannahs-place/3.jpg);
		padding: 6% 0 0 0;
	}

  #section4{
    background-image: url(/img/at-hannahs-place/4.jpg);
    padding: 6% 0 0 0;
  }


</style>

<div id="fullpage">
	<div class="section" id="section0"><h1>Best Friends</h1></div>
	<div class="section" id="section2"><h1>Lovely Smile</h1></div>
	<div class="section" id="section3"></div>
  <div class="section" id="section4"></div>
</div>

<script type="text/javascript">
		$(document).ready(function() {
			$('#fullpage').fullpage({
				'verticalCentered': false,
				navigation: true,
                autoScrolling: true,
                scrollingSpeed: 1200
			});
		});
	</script>
