Howtodo - Application - Eclipse Tuning
======================================

#### Tweak eclipse.inifile
----

	-Xverify:none
	-Xms128m
	-Xmx1024m
	-Xmn256m
	-XX:+AggressiveOpts
	-XX:PermSize=128m
	-XX:MaxPermSize=256m
	-XX:+UseParallelGC
	-XX:+UseParallelOldGC


#### Tweak Eclipse Preferences
----

	General > Startup and Shutdown
		-  Remove all plugins activated on startup
	General > Editors > Text Editors > Spelling 
		- Uncheck - Enable spell checking
	General > Validation
		- Check - Suspend all validators
	Install/Update > Automatic Updates
		- Uncheck - Automatically find new updates and notify me
	General > Appearance
		- Uncheck - Enable Animations
	Java > Editor > Content Assist 
		- Uncheck - Enable auto activation
	Java > Editor > Content Assist > Advanced
	 	- Uncheck unwanted content assist
  


#### Source
----
[7 Tips to Speed Up Eclipse](http://www.nicolasbize.com/blog/7-tips-to-speed-up-eclipse/)

