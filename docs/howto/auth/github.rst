.. _howto/auth/github:

===================================
Authenticate using GitHub Usernames
===================================

The **GitHub Authenticator** lets users log into your JupyterHub using their
GitHub user ID / password. To do so, you'll first need to register an
application with GitHub, and then provide information about this
application to your ``tljh`` configuration.

Enabling the authenticator
==========================

.. note::

   You'll need a GitHub account in order to complete these steps.

#. Create a GitHub application
   #. Go to the `GitHub OAuth app creation page <https://github.com/settings/applications/new>`_.
   #. **Application name**: Choose a descriptive application name (e.g. ``tljh``)
   #. **Homepage URL**: Use the IP address or URL of your JupyterHub. e.g. ``http://<my-tljh-url>```.
   #. **Application description**: Use any description that you like.
   #. **Authorization callback URL**: Insert text with the following form::

      http://<my-tljh-url>/hub/oauth_callback

   #. When you're done filling in the page, it should look something like this:

      .. image:: ../../images/auth/github/create_application.png
         :alt: Create a GitHub OAuth application
   #. Click "Register application".
   #. You'll be taken to a page with the registered application details. Note
      the **Client ID** and **Client Secret**, as you will use these later.

      .. image:: ../../images/auth/github/client_id_secret.png
        :alt: Your client ID and secret

#. Configure your JupyterHub to use the GitHub Oathenticator
   #. Log in as an administrator account to your JupyterHub.
   #. Open a terminal on your JupyterHub.
   #. Configure the GitHub OAuthenticator to use your client ID and secret with the following commands::

        sudo -E tljh-config set auth.GitHubOAuthenticator.client_id '<my-tljh-client-id>'
        sudo -E tljh-config set auth.GitHubOAuthenticator.client_secret '<my-tljh-client-secret>'

   #. Tell your JupyterHub to *use* the GitHub OAuthenticator for authentication::

        sudo -E tljh-config set auth.type oauthenticator.github.GitHubOAuthenticator

   #. Restart your JupyterHub so that new users see these changes::

        sudo -E tljh-config reload
#. Confirm that the new authentactor works.
   #. Open an **incognito window** in your browser.
   #. Go to your JupyterHub URL.
   #. You should see a GitHub login button like below:

      .. image:: ../../images/auth/github/client_id_secret.png
         :alt: The GitHub authenticator login button.
