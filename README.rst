Turns out automating SSL certs for dockers on your machine can be done
in minutes!

Steps:

1. Change the email in the docker-compose.yml file to your own.
2. Run ``docker-compose up -d`` in this directory.
3. Add some things to containers that you create:

  *  ``VIRTUAL_HOST``, ``VIRTUAL_PORT``, and ``LETSENCRYPT_HOST``
     environment variables to any containers you create. Example:

      .. code:: yaml

          environment:
            VIRTUAL_HOST: finally.example.com
            VIRTUAL_PORT: "80"
            LETSENCRYPT_HOST: finally.example.com

  *  Make sure ``VIRTUAL_PORT`` is exposed either via the Dockerfile or
     your compose config:

      .. code:: yaml

          expose:
            - "80"

4. If you are using compose to spin up containers or host docker network
   mode, you will need to connect ``nginx-proxy`` to those networks
   manually; otherwise, you will notice 502 errors because the proxy
   cannot communicate with things outside of its network. For example,
   ``docker network connect finally_default nginx-proxy``. (Note:
   ``docker network ls`` may be useful to you here.)
5. That is it! Enjoy! If something happens feel free to leave an issue,
   or even better open a PR to fix it.
