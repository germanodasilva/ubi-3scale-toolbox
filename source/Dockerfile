FROM registry.access.redhat.com/ubi8:8.10-1088

ENV 3SCALE_VERSION=2.6 \
    TOOLBOX_VERSION=0.20.0 \
    NAME=3scale-toolbox

ENV SUMMARY="Platform for automating the API publishing process in 3Scale." \
    DESCRIPTION="O 3scale é uma plataforma de gerenciamento de APIs desenvolvida pela Red Hat. \
                Ela permite que empresas controlem, distribuam e monitorem suas APIs, oferecendo funcionalidades como \
                autenticação, controle de tráfego, monetização e análise de uso. O 3scale facilita a integração de APIs com segurança e escalabilidade \
                permitindo maior controle sobre o acesso e o desempenho das APIs."

LABEL summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.description="${DESCRIPTION}" \
      io.k8s.display-name="ubi9 with ${NAME} ${TOOLBOX_VERSION}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,${NAME}" \
      name="ubi9/${NAME}-${TOOLBOX_VERSION}" \
      com.redhat.component="${NAME}-${TOOLBOX_VERSION}-container" \
      version="1" \
      com.redhat.license_terms="https://www.redhat.com/en/about/red-hat-end-user-license-agreements#UBI" \
      help="For more information visit https://github.com/germanodasilva/ubi-3scale-toolbox" \
      usage="podman build https://github.com/germanodasilva/ubi-3scale-toolbox.git" \
      maintainer="Germano Da Silva <gedasilv@redhat.com>"

# Install components      
RUN subscription-manager register --username=${USER_SUBSCRIPTION} --password=${PASS_SUBSCRIPTION} && \
    dnf update -y && \
    #dnf groupinstall "Development Tools" -y
    dnf install wget curl git -y && \
    cd /opt && \
    wget https://github.com/3scale-labs/3scale_toolbox_packaging/releases/download/v0.20.0/3scale-toolbox-0.20.0-1.el8.x86_64.rpm && \
    rpm -i 3scale-toolbox-0.20.0-1.el8.x86_64.rpm && \
    wget https://mirror.openshift.com/pub/openshift-v4/x86_64/clients/ocp/stable/openshift-client-linux.tar.gz && \
    tar -zxvf openshift-client-linux.tar.gz -C /usr/sbin
    