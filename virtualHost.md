# Setting up Virtual host for Windows

## Step 1

1. go to C:\WINDOWS\system32\drivers\etc\
1. Open the "hosts" file and  insert:

* ```xml
  127.0.0.1       localhost
  127.0.0.1       test.com
  127.0.0.1       example.com
  ```

## Step 2

1. go to xampp\apache\conf\extra\httpd-vhosts.conf

* ```xml
    <VirtualHost *:80>
    DocumentRoot C:/xampp/htdocs/test/
    ServerName example.com
    </VirtualHost>
  ```

## Step 3

1. go to C:\xampp\apache\conf\httpd.conf
2. find Supplemental configuration section at the end, and locate the following section (around line 500), Remove the # from the beginning of the second line so the section now looks like this:

* ```
    #Virtual hosts
    Include conf/extra/httpd-vhosts.conf
  ```

## Step 4

1. Restart XAMPP and now run in your browser :

* ```
    example.com
  ```

  # Setting up Virtual host for Linux

  ## Step 1

  1. go to /etc/
  1. Open the "hosts" file and  insert:

  * ```
    127.0.0.1       localhost
    127.0.0.1       test.com
    127.0.0.1       example.com //this is another website
    ```

  ## Step 2

  1. go to /opt/lamp/etc/extra/httpd-vhosts.conf

  * ```
      <VirtualHost *:80>
        DocumentRoot "/opt/lamp/htdocs/test"
        ServerName test.com
      </VirtualHost>
    ```
  2. Be sure to have this in the end of the document:

    * ```
    <VirtualHost *:80>
      DocumentRoot "/opt/lamp/htdocs/"
    </VirtualHost>
    ```

  ## Step 3

  1. go to /opt/lamp/etc/httpd.conf
  2. find Supplemental configuration section at the end, and locate the following section (around line 500), Remove the # from the beginning of the second line so the section now looks like this:

  * ```
      #Virtual hosts
      Include conf/extra/httpd-vhosts.conf
    ```

  ## Step 4

  1. Restart XAMPP and now run in your browser :

  * ```
      www.test.com
    ```