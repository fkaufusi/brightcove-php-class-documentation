# brightcove-php-class-documentation
Documentation about brightcove php wrapper class in https://github.com/brightcove/PHP-API-Wrapper

# PHP Wrapper for the Brightcove API

## Installation notes

This library requires PHP 7.1 or newer with a CURL extension. You have to run `composer install` before using the library.

    # apt-get install php5 php5-curl curl

    PHP-API-Wrapper$ curl -sS https://getcomposer.org/installer | php

    PHP-API-Wrapper$ php composer.phar install

## Testing notes

Running the tests requires a `config.json` file. There's a sample file included in the repository.

A reverse SSH tunnel is needed for the DI API test. When you set it up, make sure that the port is open on the remote
server too.

Example script:

    #!/bin/sh
    
    ssh -nNT -R 8888::8888 example.com &>ssh_tunnel_logfile.txt &
    PID=$!
    
    cleanup () {
        kill ${PID}
        cat ssh_tunnel_logfile.txt
        rm ssh_tunnel_logfile.txt
    }
    
    handle_error () {
        cleanup
        exit 1
    }
    
    ./vendor/bin/phpunit
    
    cleanup

## How to use this PHP Wrapper class
Example list of videos


    use Brightcove\API\CMS;
    use Brightcove\API\Client;
    
    $client_secret = 'LSkjsdlj9sdfjsldkj3fa3dsfsadf343asdf3a';
    $account_id = '7878784548743';
    $client_id = '45kh42-sgf98-sd873-33sdf-fkjsdf8474';

    $client = Client::authorize($client_id, $client_secret);
    $a = new CMS($client, $account_id);
    $result = $a->listVideos();

    
 Now you can do whatever you want with the result variable which has list of videos from Brightcove.
