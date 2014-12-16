
# Syntax based normalization of URI's

This normalizes URI's based on the specification RFC 3986 
http://www.apps.ietf.org/rfc/rfc3986.html

Example usage:

	require_once 'vendor/autoload.php';

	$url = 'eXAMPLE://a/./b/../b/%63/%7bfoo%7d';
	$un = new URL\Normalizer( $url );
	echo $un->normalize();

	// result: "example://a/b/c/%7Bfoo%7D"

The normalization process preserves semantics so, for example, the following URL's are all equivalent:

HTTP://www.Example.com/ and http://www.example.com/
http://www.example.com/a%c2%b1b and http://www.example.com/a%C2%B1b
http://www.example.com/%7Eusername/ and http://www.example.com/~username/
http://www.example.com and http://www.example.com/
http://www.example.com:80/bar.html and http://www.example.com/bar.html
http://www.example.com/../a/b/../c/./d.html and http://www.example.com/a/c/d.html
http://www.example.com/?array[key]=value and http://www.example.com/?array%5Bkey%5D=value

The following normalizations are performed:

1. Converting the scheme and host to lower case
2. Capitalizing letters in escape sequences
3. Decoding percent-encoded octets of unreserved characters
4. Adding trailing /
5. Removing the default port
6. Removing dot-segments

For more information about these normalizations, please see the following Wikipedia article:

http://en.wikipedia.org/wiki/URL_normalization#Normalizations_that_Preserve_Semantics

For license information, please see LICENSE file.

## TODO

Add further scheme-based normalization steps, as detailed in section 6.2.3 of the RFC.
