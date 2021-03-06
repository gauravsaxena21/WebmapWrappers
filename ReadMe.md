# WebMap Wrapper Project

## Features

The WebMap Wrapper serves as a foundational python sample that allows for modifying webmap JSON prior to executing a print task. This pre-processing is intended to occur server-side within a geoprocessing service. There are two situations for which this project is written. 

### Replace Service Paths

The first scenario is that the Webmap JSON may reference internal services using external paths. This situation rises when someone builds a custom application and configures a print service for that application. In many cases, the print request is sent by the application to a Print Service that resides on the same server that the Map Services and Feature Services in the webmap are served from. But since the paths are public-facing, the Print Service then has to make requests that leave the internal network and then come back in. Along with the sheer inefficiency of these requests, many network configurations may block this kind of traffic. The solution is to use a wrapper that parses the Webmap JSON and, when appropriate, substitutes the public-facing paths with internal ones. This JSON is then sent to the desired print task.

### Insert Token

The other scenario involves printing secured services. If the application uses a proxy page, the tokens acquired by the proxy page will not accompany the webmap JSON in the request. Further, if long-lived tokens are stored within the application, these tokens will not be valid when used by the print service. The documented solution to this scenario is outlined in the following Help Document provided by Esri.

Printing maps that contain secured services
http://resources.arcgis.com/en/help/main/10.1/index.html#//0154000005q3000000

However, due to a bug, specific layer references in the webmap JSON will not get a token.

*[#NIM094431  A custom print service with saved credentials created from the Export Web Map task fails to print individual feature layers from a secured map service. ]*

This python wrapper has the ability to retrieve a short-lived token for services residing on a specific server, and append that token to the service references in the webmap JSON. Conceptually, this is the same functionality that proxy pages provide applications (hidden service authentication), but specifically for print services.

**Security considerations:**

* The username and password to ArcGIS Server are explicitly configured within the python script. If security is a consideration, it will be necessary to take any necessary precautions to prevent the reproduction of the script.

* As currently configured, the script determines the token service URL from the rest/info page. This means that if SSL is not configured on your server, the username and password will be passed to AGS unencrypted and could potentially be intercepted by a third party. When externalizing your services, always authenticate using HTTPS to encrypt the credentials.

## Instructions

Please consult the ReadMe in each project section for specific instructions

## Requirements

* ArcGIS Desktop 10.2 or higher
* ArcGIS Server 10.2 or higher

## Issues

If you find a bug or think of a new feature you'd like to see, please let be know by submitting an issue.

## Contributing

I follow the Esri Github guidelines for contributing. Please see [guidelines for contributing](https://github.com/esri/contributing).

## Licensing

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at


   http://www.apache.org/licenses/LICENSE-2.0


Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


A copy of the license is available in the repository.
