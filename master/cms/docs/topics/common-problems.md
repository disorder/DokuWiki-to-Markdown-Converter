# Common Problems

From time to time, things will go wrong.  Here's a few things to try when you're confused.

## The output shows only "Website Error"

TODO

## My templates don't update on page refresh

Putting ?flush=1 on the end of any SilverStripe URL will clear out all cached content; this is a pretty common solution
to a lot of development problems.  Here are some specifics situations:

*  You've created a new SS or PHP file
*  You've edited a nested template (one inserted with the <% include %> tag)
*  You've published a new copy of your site
*  You've upgraded your version of SilverStripe

## A SQL query fails with "Column not found" or "Table not found"

Whenever you change the model definitions in PHP (e.g. when adding a property to the [$db](api:DataObject::$db) array,
creating a new page type), SilverStripe will need to update the database. Visiting `http://<my-domain>/dev/build` in
your browser runs a script that will check the database schema and update it as necessary.  Putting `?flush=1` on the
end makes sure that nothing that's linked to the old database structure will be carried over.  If things aren't saving,
pages aren't loading, or other random things aren't working it's possible that the database hasn't been updated to
handle the new code.  Here are some specifics situations:

*  You've created a new page type / other data object type
*  You've change the type of one of your database fields
*  You've published a new copy of your site
*  You've upgraded your version of SilverStripe

## My edited CMS content doesn't show on the website

If you've set up your site and it used to be working, but now it's suddenly totally broken, you may have forgotten to
publish your draft content.  Go to the CMS and use the "publish" button.  You can visit `admin/publishall` to publish
every page on the site, if that's easier.

## I can see unparsed PHP output in my browser

Please make sure all code inside '*.php' files is wrapped in classes. Due to the way [ManifestBuilder](ManifestBuilder)
includes all files with this extension, any **procedural code will be executed on every call**. Most common error here
is putting a test.php/phpinfo.php file in the document root. See [datamodel](datamodel) and [controllers](controllers)
for ways how to structure your code.

## I've got file permission problems during installation

The php installer needs to be able write files during installation, which should be restricted again afterwards. It
needs to create/have write-access to:

 * The main installation directory (for creating .htaccess file and assets directory)
 * The mysite folder (to create _config.php)
 * After the install, the assets directory is the only directory that needs write access.
 * Image thumbnails will not show in the CMS if permission is not given 