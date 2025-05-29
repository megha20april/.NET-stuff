Connected Services
- through this file we can integrate external services, APIs, and cloud-based solutions.
- It allows developers to connect their application to various service providers like Azure, AWS, Google Cloud, and third-party authentication providers or databases.
- Provides a centralized location to manage all connected services.
- try it with examples and understand what exactly does it do

Dependencies
- add our nuget packages

Properties/launchSettings.json
- $schema: defines the format of launchSettings.json file, hence it allows us to edit this file by ensuring ide understands this file.
- iis -> internet information service used for running and testing applications locally without hosting it on a separate server.
- 


wwwroot
- serves static files, you can access them like this, `<localhostUrl>/js/site.js` etc.
- these files are not critical and is genrally client side
- also images, fonts or any other assets.
- also handles their caching.

