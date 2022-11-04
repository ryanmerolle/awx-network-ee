ARG EE_BASE_IMAGE=ghcr.io/ryanmerolle/ansible-runner:stable-2.12
ARG EE_BUILDER_IMAGE=ghcr.io/ryanmerolle/ansible-builder:latest

FROM $EE_BASE_IMAGE as galaxy
USER root

ADD _build /build
WORKDIR /build

RUN ansible-galaxy role install -r requirements.yml --roles-path "/usr/share/ansible/roles"
RUN ANSIBLE_GALAXY_DISABLE_GPG_VERIFY=1 ansible-galaxy collection install -r requirements.yml --collections-path "/usr/share/ansible/collections"

FROM $EE_BUILDER_IMAGE as builder

COPY --from=galaxy /usr/share/ansible /usr/share/ansible

ADD _build/requirements.txt requirements.txt
RUN ansible-builder introspect --sanitize --user-pip=requirements.txt --write-bindep=/tmp/src/bindep.txt --write-pip=/tmp/src/requirements.txt
RUN assemble

FROM $EE_BASE_IMAGE
USER root

COPY --from=galaxy /usr/share/ansible /usr/share/ansible

COPY --from=builder /output/ /output/
RUN /output/install-from-bindep && rm -rf /output/wheels
RUN ansible-galaxy collection install arista.avd -p /usr/share/ansible/collections/ansible_collections
LABEL ansible-execution-environment=true
