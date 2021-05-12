# laravel formation

channel youtube of creator : Nord Coders https://www.youtube.com/channel/UC36hi0WMeiR8HpUy-A2s4vQ

link playlist laravel class : https://www.youtube.com/watch?v=2m-A0PYuj6E&list=PLeeuvNW2FHVgvC-PdSfi309DbDMoEswiT

thanks to the youtuber "Nord Coders" ^^


first of all
--------------

- use windows 10
- install 1 text editor for coders (ex: vs code, sublime)
- install the "laragon" development stack : https://sourceforge.net/projects/laragon/files/releases/4.0/laragon-full.exe/download
- if you want another php version for windows (version 8) go : https://windows.php.net/download#php-8.0
	<br/>&emsp;. download the zip win32 x64 version if you are in 64 bits and prefere safe version
	<br/>&emsp;. go to laragon/bin/php and extract the zip in a folder with the zip name
	<br/>&emsp;. open laragon, menu -> php/version/ choose the new one
	<br/>&emsp;. make sure you you are running with the new php version, check in the laragon terminal 
		<br/>&emsp;&emsp; -> php -v. Restart laragon if it isn't the case, then "start all" in laragon and go "web"
- install the "composer" dependency manager for php  : https://getcomposer.org/
	<br/>&emsp;. select the good path with the php version you want to use -> laragon/bin/php/version you want/php.exe
- open laragon -> terminal
	<br/>&emsp;. tape command line : composer global require laravel/installer
	<br/>&emsp;. copy path generated on the console : C:/Users/username/AppData/Roaming/Composer (in this case)
- go to environment path
	<br/>&emsp;.on the top -> new
		<br/>&emsp;&emsp;variable name : LaravelInstaller
		<br/>&emsp;&emsp;variable value : paste the copied path with additional values on the end "/vendor/bin"
			<br/>&emsp;&emsp;&emsp;-> C:/Users/username/AppData/Roaming/Composer/vendor/bin
- close and reopen terminal
	<br/>&emsp;. tape command lines :
		<br/>&emsp;&emsp;- rm index.php
		<br/>&emsp;&emsp;- laravel new blog
- change the home page -> menu laragon/www/switch document root -> laragon/www/blog/public
