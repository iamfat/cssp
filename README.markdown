# Usage
	include “cssp.php”;
	$css = file_get_contents('path/to/file.css');
	echo CSSP::fragment($css)->format(CSSP::FORMAT_NOCOMMENTS);  // CSSP::FORMAT_NOCOMMENTS || CSSP::FORMAT_MINIFY

# Syntax
## Variables
BEFORE

	@css-define lightblue:"#336699";
	.text {
		color: $lightblue;
	}

AFTER

	.text {
		color: #336699;
	}


## CSS3 Patch
BEFORE

	div { border-radius: 3px; }
	div.test {border-radius: 3px 3px 0 0; }

AFTER

	div {
		-webkit-border-radius: 3px;
		-moz-border-radius: 3px;
		border-radius: 3px;
	}

	div.test {
		-webkit-border-top-left-radius: 3px;
		-webkit-border-top-right-radius: 3px;
		-webkit-border-bottom-right-radius: 0;
		-webkit-border-bottom-left-radius: 0;
		-moz-border-radius: 3px 3px 0 0;
		border-radius: 3px 3px 0 0;
	}

## Nested Rules
BEFORE

	#header, #footer {
	  color: red;
	  a {
		font-weight: bold;
		text-decoration: none;
		&:hover {
		  color: red;
		}
	  }
	}

AFTER

	#header, #footer {
		color: red;
	}


	#header a,  #footer a {
		font-weight: bold;
		text-decoration: none;
	}


	#header a:hover,   #footer a:hover {
		color: red;
	}
