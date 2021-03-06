source: Developing/Code-Structure.md
path: blob/master/doc/
# Code structure.

This document will try and provide a good overview of how the code is structured within LibreNMS. We will go through the main directories and provide information on how and when they are used.
LibreNMS now uses [Laravel](https://laravel.com/docs/) for much of it's frontend (webui) and database code. Much of the Laravel documentation applies: https://laravel.com/docs/structure

### doc/
This is the location of all the documentation for LibreNMS, this is in GitHub markdown format and can be viewed [online](http://docs.librenms.org/)

### app/
Most Laravel and Eloquent classes should be under this directory.

### LibreNMS/
Classes that don't belong to the Laravel application belong in this directory, with a directory structure that matches the namespace.  One class per file. See [PSR-0](http://www.php-fig.org/psr/psr-0/) for details.

### html/
All legacy web accessible files are located here. New pages should follow the Laravel conventions.
### html/api_v0.php
This is the API routing file which directs users to the correct API function based on the API endpoint call.
### html/index.php
This is the main file which all links within LibreNMS are parsed through. It loads the majority of the relevant includes needed for the control panel to function. CSS and JS files are also loaded here.
### html/css
All used css files are located here.
### html/css/custom
This is a folder you can put custom css files into that won't interfere with auto updates
### html/forms
This folder contains all of the files that are dynamically included from an ajax call to ajax/form.
### html/includes
This is where the majority of the website core files are located. These tend to be files that contain functions or often used code segments that can be included where needed rather than duplicating code.
### html/includes/api_functions.inc.php
All of the functions and calls for the API are located here.
### html/includes/authenticate.inc.php, html/includes/authentication/
These files are what provides the authentication layer to the user. In the folder are separate files based on the auth type used, this means new authentication types can be added easily enough.
### html/includes/functions.inc.php
This contains the majority of functions used throughout the standard web ui.
### html/includes/reports/
In here is a list of of files that generate PDF reports available to the user. These are dynamically called in from html/pdf.pdf based on the report the user requests.
### html/includes/table/
This folder contains all of the ajax calls when generating the table of data. Most have been converted over so if you are planning to add a new table of data then you will do so here for all of the back end data calls.
### html/js/
All used JS files are located here.
### html/pages
This folder contains the URL structure when browsing the Web UI. So for example /devices/ is actually a call to html/pages/devices.inc.php, /device/tab=ports/ is html/pages/device/ports.inc.php.

### includes/
This folder is quite big and contains all the files to make the cli and polling / discovery to work.  This code is not currently accessible from Laravel code (intentionally).
### includes/discovery/, includes/polling/
All the discovery and polling code. The format is usually quite similar between discovery and polling. Both are made up of modules and the files within the relevant directories will match that module. So for instance if you want to update the os detection for a device, you would look in includes/discovery/os/ for a file named after the operating system such as linux: includes/discovery/linux.inc.php. Within here you would update or add support for newer OS'. This is the same for polling as well.

### logs/
Contains the main librenms.log file by default, but can also contain your web server's logs, poller logs, and other items.

### mibs/
Here is where all of the mibs are located.  Generally standard mibs should be in the root directory and specific vendor mibs should be in their own subdirectory.

### rrd/
Simple enough, this is where all of the rrd files are created. They are stored in folders based on the device hostname.

### database/migrations
Contains all the database migrations.  See Laravel docs for additional info: https://laravel.com/docs/migrations
