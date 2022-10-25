# Get Started Docker on Ubuntu 22.04

## Latihan 2

# Start the tutorial

    $ docker run -d -p 80:80 docker/getting-started
    
    You’ll notice a few flags being used. Here’s some more info on them:

    -d - Run the container in detached mode (in the background).
    -p 80:80 - Map port 80 of the host to port 80 in the container. To access the tutorial, open a web browser and navigate to http://localhost:80. If you already have a service listening on port 80 on your host machine, you can specify another port. For example, specify -p 3000:80 and then access the tutorial via a web browser at http://localhost:3000.
    docker/getting-started - Specify the image to use.

You can combine single character flags to shorten the full command. As an example, the command above could be written as:

    docker run -dp 80:80 docker/getting-started
    
Credentials management for Linux users
Docker Desktop relies on pass to store credentials in gpg2-encrypted files. Before signing in to Docker Hub from the Docker Dashboard or the Docker menu, you must initialize pass. Docker Desktop displays a warning if you’ve not initialized pass.

You can intialize pass by using a gpg key. To generate a gpg key, run:
    
    $ gpg --generate-key
    
To initialize pass, run:

    $ pass init 186159A79ACDB6F490802A372547A27FE2205003
    
Once pass is initialized, you can sign in on the Docker Dashboard and pull your private images. When credentials are used by the Docker CLI or Docker Desktop, a user prompt may pop up for the password you set during the gpg key generation.

    $ docker pull molly/privateimage


  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
