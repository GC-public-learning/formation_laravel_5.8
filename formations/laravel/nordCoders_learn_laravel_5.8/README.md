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
	\&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp . download the zip win32 x64 version if you are in 64 bits and prefere safe version
	\&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp . go to laragon/bin/php and extract the zip in a folder with the zip name
	\&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp . open laragon, menu -> php/version/ choose the new one
- install the "composer" dependency manager for php  : https://getcomposer.org/
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp. select the good path with the php version you want to use -> laragon/bin/php/version you want/php.exe
- open laragon -> terminal
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp . tape command line : composer global require laravel/installer
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp . copy path generated on the console : C:/Users/jo/AppData/Roaming/Composer (in this case)
- go to environment path
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp.on the top -> new
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbspvariable name : LaravelInstaller
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbspvariable value : paste the copied path with additional values on the end "/vendor/bin"
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp-> C:/Users/jo/AppData/Roaming/Composer/vendor/bin
- close and reopen terminal
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp. tape command lines :
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp- rm index.php
		&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp- laravel new blog
- change the home page -> menu laragon/www/switch document root -> laragon/www/blog/public
