There will be other simpler queue methods added soon, but for now PHP was the quickest way to the goal. As you can see the simplicity of it you can get an idea for how to replace it with something you like better. I will be working on a DynamoDB queue using lambda to replace this.

This PHP implementation isn't the most secure out of the box, so you'll want to keep the URLs private at the very least and consider adding authentication to the files, but in order to do that you'd need to modify the Python code for Kali and the Alexa Node code. You will want to change the filenames to something unique to you and mod the lines in the Python and the Lambda config to point to the right queue pages. You probably should even go so far as to change the filenames in code to where the queue data is saved. This way, nobody will infer the location of your requests. (Not that they are super revealing) In the next rev I anticipate adding encryption and enabling the signing.

A slight improvement in security can be achieved by adding headers to the files served by your web server so that there is less chance for the queue file to be interpreted.

Each web server will have some equivalent to this blanket application of headers method. (Google is your friend)

If hosting on Apache you should have mod_headers enabled and add the following block of headers to your .htaccess file (don't include the ----- snip ----- lines)
Note, that adding the SAMEORIGIN frame header will break most iframing schemes so if you are crazy and want people to iframe your stuff from another domain, then by all means you're welcome to take that one out. But with any change to web server config file work, save your original just in case testing shows you're broken.

Again: below is a snip from a .HTACCESS file for Apache designed to take effect if mod_headers is installed.
----- snip ------
<IfModule mod_headers.c>
	Header set X-XSS-Protection "1; mode=block"
	Header always append X-Frame-Options SAMEORIGIN
	Header set X-Content-Type-Options nosniff
</IfModule>
----- snip -------




    HackerMode 2 basic PHP queue
    Copyright (C) 2019  David Cross

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.