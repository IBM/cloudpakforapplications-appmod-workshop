# IBM Skills Network Access

## Access IBM Skills Network

1. If you have registered your account, you can access the lab environment at **https://labs.cognitiveclass.ai/** and go directly to step 6.

1. Navigate to https://labs.cognitiveclass.ai/register,

    ![Cognitive Class button](../.gitbook/generic/cogClassButton.png)

1. Create a new account with a Social login (LinkedIn, Google, Github or Facebook), or click the `Cognitive Class` button,

    ![Cognitive Class button](../.gitbook/generic/cogClassButton2.png)

1. Click `Create an Account`,

1. Fill in your Email, Full Name, Public Username and password, click on the check boxes next to the `Privacy Notice` and `Terms of Service` to accept them. Then click on `Create Account`.

1. You will then be taken to a page with a list of sandbox environments. Click on the option for **Theia - Cloud IDE (With OpenShift)**

    ![sandbox list](../.gitbook/generic/sandboxList.png)

1. Wait a few minutes while your environment is created.

    ![waiting](../.gitbook/generic/waiting.png)

1. You will be taken to a blank editor page once your environment is ready.

1.  What we really need is access to the terminal. Click on the `Terminal` tab near the top of the page and select **New Terminal**

    ![New Terminal](../.gitbook/generic/newTerminal.png)

1.  You can then click and drag the top of the terminal section upwards to make the terminal section bigger.

    ![bigger terminal](../.gitbook/generic/biggerTerminal.png)

## Install s2i CLI tool

To install s2i CLI tool,

1. Download tar file.

    ```
	curl -s https://api.github.com/repos/openshift/source-to-image/releases/latest \
	  | grep browser_download_url \
	  | grep linux-amd64 \
	  | cut -d '"' -f 4 \
	  | wget -qi -
    ```

1. Unzip tar file

    ```
	tar xvf source-to-image*.gz
    ```

1. Make s2i CLI accessiblee.

    ```
	sudo mv s2i /usr/local/bin
    ```

1. verify

    ```
	s2i version  
    ```


With that done, you can start the lab.



