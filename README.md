
# Getting Started with auth

## Building

The generated code has dependencies over external libraries like UniRest. These dependencies are defined in the `composer.json` file that comes with the SDK. To resolve these dependencies, we use the Composer package manager which requires PHP greater than or equal to 7.2 installed in your system. Visit [https://getcomposer.org/download/](https://getcomposer.org/download/) to download the installer file for Composer and run it in your system. Open command prompt and type `composer --version`. This should display the current version of the Composer installed if the installation was successful.

* Using command line, navigate to the directory containing the generated files (including `composer.json`) for the SDK.
* Run the command `composer install`. This should install all the required dependencies and create the `vendor` directory in your project directory.

![Building SDK - Step 1](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=installDependencies)

### Configuring CURL Certificate Path in php.ini

:information_source: **Note** This is for Windows users only.

CURL used to include a list of accepted CAs, but no longer bundles ANY CA certs. So by default it will reject all SSL certificates as unverifiable. You will have to get your CA's cert and point curl at it. The steps are as follows:

1. Download the certificate bundle (.pem file) from [https://curl.haxx.se/docs/caextract.html](https://curl.haxx.se/docs/caextract.html) on to your system.
2. Add curl.cainfo = "PATH_TO/cacert.pem" to your php.ini file located in your php installation. “PATH_TO” must be an absolute path containing the .pem file.

```
[curl]; A default value for the CURLOPT_CAINFO option. This is required to be an
; absolute path.
curl.cainfo = PATH_TO/cacert.pem
```

## Installation

The following section explains how to use the AuthLib library in a new project.

### 1. Open Project in an IDE

Open an IDE for PHP like PhpStorm. The basic workflow presented here is also applicable if you prefer using a different editor or IDE.

![Open project in PHPStorm - Step 1](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=openIDE)

Click on `Open` in PhpStorm to browse to your generated SDK directory and then click `OK`.

![Open project in PHPStorm - Step 2](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=openProject0)

### 2. Add a new Test Project

Create a new directory by right clicking on the solution name as shown below:

![Add a new project in PHPStorm - Step 1](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=createDirectory)

Name the directory as "test".

![Add a new project in PHPStorm - Step 2](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=nameDirectory)

Add a PHP file to this project.

![Add a new project in PHPStorm - Step 3](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=createFile)

Name it "testSDK".

![Add a new project in PHPStorm - Step 4](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=nameFile)

Depending on your project setup, you might need to include composer's autoloader in your PHP code to enable auto loading of classes.

```php
require_once "vendor/autoload.php";
```

It is important that the path inside require_once correctly points to the file `autoload.php` inside the vendor directory created during dependency installations.

![Add a new project in PHPStorm - Step 5](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=projectFiles)

After this you can add code to initialize the client library and acquire the instance of a Controller class. Sample code to initialize the client library and use the Controller methods is given in the subsequent sections.

### 3. Run the Test Project

To run your project you must set the Interpreter for your project. Interpreter is the PHP engine installed on your computer.

Open `Settings` from `File` menu.

![Run Test Project - Step 1](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=openSettings)

Select `PHP` from within `Languages & Frameworks`.

![Run Test Project - Step 2](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=setInterpreter0)

Browse for Interpreters near the `Interpreter` option and choose your interpreter.

![Run Test Project - Step 3](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=setInterpreter1)

Once the interpreter is selected, click `OK`.

![Run Test Project - Step 4](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=setInterpreter2)

To run your project, right click on your PHP file inside your Test project and click on `Run`.

![Run Test Project - Step 5](https://apidocs.io/illustration/php?workspaceFolder=Auth&step=runProject)

## Initialize the API Client

**_Note:_** Documentation for the client can be found [here.](/doc/client.md)

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| `authorization` | `string` | *Default*: `'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIxMyIsImp0aSI6Ijk4OGNiM2E2OTc0NjMxOTQwMWI5ODczNjA2YjU1N2U0MTNmNmViNjQ3MjlhZmM2ZTQzZTExY2JkM2YxNmYzYzRkMzM5ZDg2ZGE4ZTVmMTkyIiwiaWF0IjoxNjM0NTYwMjY2Ljk4NzMzNzExMjQyNjc1NzgxMjUsIm5iZiI6MTYzNDU2MDI2Ni45ODczNDA5MjcxMjQwMjM0Mzc1LCJleHAiOjE2NjYwOTYyNjYuOTg0MDY2MDA5NTIxNDg0Mzc1LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.lbnBies2oy0H4kGu0QY5O2YZgng6bFbsaukFQ1meQfMGJ22ka3e-p6mK8xWwbs4Pxw1d1BWtj54fH7GnETUipN0CI10R64qX6DzqUWtMaX_lw5HgdUSwDXy9Vw3ZuGctCErKbQtKhdFTUbXvtAuodj6aXfdwmMsicNTBnYuLMnxfFfKs7Df8rHHH0ZxdxxWF1ZwqqQ3-qtG_lhOoz18Ux7ZHA20xkGjC6i_NugsQfpgZpel20A7nYCaqPHNCDC-yukN5DjaF2MIlE2wkz5ib6uTnHOBSCuvf-WGdRaDM1Un-S_-3XuaJjdBIMN_BvbWEKihe_zyR8o1V_288vqy6HuwmuDjwJi0_Yv-H0EytBDBDf-kYkVx_2VZTP-4UhNxgdbgt8V_gXey-0jZx4vWz25FiQr-6oBiLvILspGp2QqQQEV5QDk6Flt8f2LMpMUQiXF3DG9D04xRP1itYZHGREwgsR4hTSWJeONULo2bH5BmZ-NBzHJucfwbmbavT09EVXbN-Mqiz4KX_dLTUaNDRRl33CqZSg8QnOBGZJ4DGSwRamBz5MLuGGkFclAdIvEEdlHrb0JnwsiC4SvoZ3FGH4CvC2kM_veqtypSoWKhN-TgJvK2T4l9jInDBBYR02eYsaIKuP5hlKPV5vSR2KSz26P6QFxCa-clUTL9ixdyMBV0'` |
| `timeout` | `int` | Timeout for API calls |

The API client can be initialized as follows:

```php
$client = new AuthLib\AuthClient([
    // Set authentication parameters
    'authorization' => 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiIxMyIsImp0aSI6Ijk4OGNiM2E2OTc0NjMxOTQwMWI5ODczNjA2YjU1N2U0MTNmNmViNjQ3MjlhZmM2ZTQzZTExY2JkM2YxNmYzYzRkMzM5ZDg2ZGE4ZTVmMTkyIiwiaWF0IjoxNjM0NTYwMjY2Ljk4NzMzNzExMjQyNjc1NzgxMjUsIm5iZiI6MTYzNDU2MDI2Ni45ODczNDA5MjcxMjQwMjM0Mzc1LCJleHAiOjE2NjYwOTYyNjYuOTg0MDY2MDA5NTIxNDg0Mzc1LCJzdWIiOiIxIiwic2NvcGVzIjpbXX0.lbnBies2oy0H4kGu0QY5O2YZgng6bFbsaukFQ1meQfMGJ22ka3e-p6mK8xWwbs4Pxw1d1BWtj54fH7GnETUipN0CI10R64qX6DzqUWtMaX_lw5HgdUSwDXy9Vw3ZuGctCErKbQtKhdFTUbXvtAuodj6aXfdwmMsicNTBnYuLMnxfFfKs7Df8rHHH0ZxdxxWF1ZwqqQ3-qtG_lhOoz18Ux7ZHA20xkGjC6i_NugsQfpgZpel20A7nYCaqPHNCDC-yukN5DjaF2MIlE2wkz5ib6uTnHOBSCuvf-WGdRaDM1Un-S_-3XuaJjdBIMN_BvbWEKihe_zyR8o1V_288vqy6HuwmuDjwJi0_Yv-H0EytBDBDf-kYkVx_2VZTP-4UhNxgdbgt8V_gXey-0jZx4vWz25FiQr-6oBiLvILspGp2QqQQEV5QDk6Flt8f2LMpMUQiXF3DG9D04xRP1itYZHGREwgsR4hTSWJeONULo2bH5BmZ-NBzHJucfwbmbavT09EVXbN-Mqiz4KX_dLTUaNDRRl33CqZSg8QnOBGZJ4DGSwRamBz5MLuGGkFclAdIvEEdlHrb0JnwsiC4SvoZ3FGH4CvC2kM_veqtypSoWKhN-TgJvK2T4l9jInDBBYR02eYsaIKuP5hlKPV5vSR2KSz26P6QFxCa-clUTL9ixdyMBV0',
]);
```

## List of APIs

* [API](/doc/controllers/api.md)

## Classes Documentation

* [Utility Classes](/doc/utility-classes.md)
* [ApiException](/doc/api-exception.md)
* [HttpRequest](/doc/http-request.md)
* [HttpResponse](/doc/http-response.md)

