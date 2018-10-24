# docker-xdebug

Integrating Docker, X-debug and PHPSTORM can be something of a task. If not for you, it was for us.

Docker containers interact with external sourc i.e. brosers for x-debug to work

Only changes you have to make is to Dockerfile and you should be ready to go

After copyimg the docker-compose file from here over to your project, follow the following steps:-

All of the docker files are stored in Docker folder created at the root of the project.
Inside the Docker folder, I have created a folder php to store all php config files.
1.	Create a Dockerfile inside Docker/php folder if not already created otherwise just add the following lines to install xdebug
                                                                               && pecl install xdebug \
&& docker-php-ext-enable xdebug \

COPY ./xdebug.ini /usr/local/etc/php/conf.d/


2.	Create a xdebug.ini file inside Docker/php
3.	Copy the following code in side xdebug.ini
zend_extension=xdebug.so

xdebug.remote_enable=1

xdebug.remote_handler=dbgp

xdebug.remote_port=9000

xdebug.remote_autostart=1

xdebug.remote_connect_back=0

xdebug.idekey="PHPSTORM"

xdebug.remote_host=It can be name of the php docker container or your ipV4 address which can be found by typing ipconfig in your command prompt. Try with either and it should work

4.	Run docker-compose up –build –d.  (xdebug configurations will be copied to php.ini )
5.	On your php storm click on File -> settings -> Languages and Frameworks ->PHP->Servers , Create a new server : host = localhost
6.	On your php storm click on File -> settings -> Languages and Frameworks ->PHP->select php language->cli interpreter and map the local path of your project to the path of docker container. 
7.	Run->Edit Configurations->create a new PHP Remote Debug->Choose a server ->ide key : PHPSTORM and click apply and then OK. 
8.	Run your xdebug now.


