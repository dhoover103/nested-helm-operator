FROM quay.io/operator-framework/helm-operator:v0.14.0

LABEL name="Owncloud Operator" \
      vendor="Bitnami" \
      version="v0.0.1" \
      release="1" \
      summary="This is an example of an owncloud helm operator." \
      description="This operator will deploy owncloud to the cluster."

COPY licenses /licenses
COPY watches.yaml ${HOME}/watches.yaml
COPY helm-charts/ ${HOME}/helm-charts/
