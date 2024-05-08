# DVWA (Damn Vulnerable Web Application)

DVWA is a deliberately vulnerable web application designed for practicing and understanding web application security. It contains various vulnerabilities that allow users to learn and experiment with different attack techniques.

## Deployment

To deploy DVWA on a local Kubernetes cluster, follow the steps below:

1. Ensure you have a local Kubernetes cluster set up (e.g., using Minikube, k3s, or any other Kubernetes distribution).

2. Apply the provided deployment and service configuration files to create the DVWA deployment and service:
    - [dvwa-deployment.yaml](dvwa-deployment.yaml)

    ```bash
    kubectl apply -f dvwa-deployment.yaml
    ```

3. Get the pod name by running:

    ```bash
    kubectl get pods
    ```

4. Since we are using Minikube, we cannot access the cluster IP directly. Forward the pod to a port:

    ```bash
    kubectl port-forward <pod_name> 8080:80
    ```

Open a web browser and enter `http://localhost:8080/` to access DVWA.

## Attack Surfaces

1. SQL Injection:
   - Access the DVWA login page and try entering the payload `' OR '1'='1` in the username or password field. This payload attempts to bypass the login mechanism by manipulating the SQL query.

2. Cross-Site Scripting (XSS):
   - Use the DVWA application's user input field vulnerable to XSS attacks to inject the payload `<script>alert('XSS');</script>`. This payload executes arbitrary JavaScript code on other users' browsers.

3. Command Injection:
   - Identify a vulnerable input field in the DVWA application and attempt to inject the payload `127.0.0.1; ls -la`. This payload aims to execute arbitrary commands on the underlying system.

## Reference

You can reference more details about DVWA vulnerabilities in the following PDF:
- [dvwa_vulnerabilities.pdf](dvwa_vulnerabilities.pdf)

The username and password for logging into DVWA application are:
- Username: admin
- Password: password

**Note**: These attack demonstrations should only be performed in a controlled and ethical environment for educational purposes.
