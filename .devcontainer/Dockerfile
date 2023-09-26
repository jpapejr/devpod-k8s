FROM --platform=linux/amd64 ubuntu:latest

ENV KUBECTL_VERSION=1.27.0
ENV IBMCLOUD_VERSION=2.20.0


RUN apt update -y && \
    apt install -y --no-install-recommends bash curl git && \
    mkdir /root/bin && \
    curl -k https://download.clis.cloud.ibm.com/ibm-cloud-cli/2.20.0/IBM_Cloud_CLI_${IBMCLOUD_VERSION}_amd64.tar.gz -o out.tar.gz && \
    tar xvzf out.tar.gz && \
    ./Bluemix_CLI/install_bluemix_cli && \
    ibmcloud plugin install container-service -r Bluemix && \
    ibmcloud plugin update container-registry -r Bluemix && \
    ibmcloud plugin install vpc-infrastructure -r Bluemix && \
    rm out.tar.gz && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
    mv kubectl /root/bin && \
    chmod +x /root/bin/kubectl

RUN echo 'export PS1="\[\e[34m\]IBM\[\e[m\]☁️  # "' > /root/.bashrc
RUN echo 'export PATH="$PATH:/root/bin"' >> /root/.bashrc
RUN echo 'cat /etc/motd' >> /root/.bashrc
RUN echo 'Thank you for using the IBM Cloud-Native Docker Container. In your first login, we suggest you ibmcloud login to authenticate against the IBM cloud API.' > /etc/motd


ENTRYPOINT ["bash"]
EXPOSE 8080-8085
