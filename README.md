# Remote Auth

Remote auth is a library for laravel api authentication or remote auth user management in web application. Its a token base authentication system that provide many functionality like blocking user between date and get login date of each valid user without any database interaction. Remote auth valid user in two way normally valid check or two way auth check let see it below.

## Getting Started

The library is designed on the focus on easly setup by any one like stratup member or expert.

### Prerequisites

You need to composer package manager for instaiig this package and their dependancy.

### Installing

Follow below step for instaiing package into laravel package


```
composer require support/remote-auth
```
Then and below line into provider array in ```config/app.php``` file

```
Support\RemoteAuth\JSRServiceProvider::class,
```

Then add into aliash array into this file.

```
'Remote' => Support\RemoteAuth\Facades\Remote::class,
```

And then publish package into laravel app.
```
php artisan vendor:publish
```
This command create ```RemoteAuth.php``` file in ```config``` folder. You can enable disable option of package using this file.

Then run following command for creating moddleware.
```
php artisan make:middleware RemoteAuth
```
And then past below code into file
```
<?php

namespace App\Http\Middleware;

use Closure;
use Remote;

class RemoteAuth
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        /*check token is received or not*/
        if(empty($request->header('Authorization'))){

            return response()->json(array('token is required'));

        /*check token is valid or not*/
        }else if($user = Remote::verify($request->header('Authorization'))){
          
            /*if valid then user data bind with request*/
            $request->r_user = $user;
        
        }else {
            
            /*if token is invalid the return invalid token error*/
            return response()->json(array('invalid token'));
        }
        
        return $next($request);
    }
}

```
No finally your api authentication is ready now regitered your middleware into your ```kernal.php``` file as your use. Generally people use route middleware so i registered them into ```kernal.php``` as route middleware.
```
 protected $routeMiddleware = [
     ...
     ...
     ...
     remote_auth' =>  \App\Http\Middleware\RemoteAuth::class
  ];
```

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
# Project Title

One Paragraph of project description goes here

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Installing

A step by step series of examples that tell you have to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
