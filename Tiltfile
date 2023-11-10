# Tiltfile

# Specify the name of your project
#name("PHP-Tilt-project")

# Define the local and remote Kubernetes context your-cluster-context depend on what you have as vcluster (in our case it is docs-vcluster2)
# make sure to choose the right Vcluster where you want to apply your tilt file

allow_k8s_contexts("docs-vcluster2")

# Specify the paths to your Kubernetes manifests
k8s_yaml("deployment-PHP-demo.yaml")
k8s_yaml("service-PHP-demo.yaml")
k8s_yaml("PHP-ingress-file.yaml")

# Add watches for file changes to trigger automatic updates
watch_file("./src/app.js")
watch_file("./src/index.php")
watch_file("./src/style.css")


