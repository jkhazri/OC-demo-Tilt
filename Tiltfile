# Tiltfile

# Specify the name of your project
name("PHP-Tilt-project")

# Define the local and remote Kubernetes context your-cluster-context depend on what you have as vcluster (in our case it is docs-vcluster2)
# make sure to choose the right Vcluster where you want to apply your tilt file

local_k8s_context("docs-vcluster2")
remote_k8s_context("docs-vcluster2")

# Specify the paths to your Kubernetes manifests
k8s_yaml("deployment-PHP-demo.yaml")
k8s_yaml("service-PHP-demo.yaml")
k8s_yaml("PHP-ingress-file.yaml")

# Add watches for file changes to trigger automatic updates
watch_file("app.js")
watch_file("index.php")
watch_file("style.css")
