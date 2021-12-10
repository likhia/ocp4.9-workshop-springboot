# This image fixes the workshop spawner and enables it to run on OpenShift 4.6
# The original image references Ingress in extensions/v1beta1

FROM quay.io/openshifthomeroom/workshop-spawner@sha256:151318399b40735c279771e9b2eb984ae74165500d7f494b8b697c1d3b7e3ead

RUN sed -i "s|api_version='extensions/v1beta1', kind='Ingress')|api_version='networking.k8s.io/v1', kind='Ingress')|" /opt/app-root/src/jupyterhub_config.py


