VERSION=v0.1.0

# For helm...
# The name of this service
SERVICE_NAME="boilerplate-echoserver"
# This is the values file which based on this (values-dev.yaml)
CI_ENVIRONMENT_SLUG="dev"
# This is the namespace to deploy to, this must exist already
K8S_NAMESPACE="dev"
# For simplicity this is the same as the above service name
HELM_CHART=${SERVICE_NAME}
CURRENT_HELM_CHART=${SERVICE_NAME}

.PHONY: all lint yamllint clean

# Need this because OS-X sed sucks, it doesn't have in-place.  If you're on OS-X and need this, you need to install homebrew and install gsed from homebrew, because OS-X's sed is "bsd" sed.  The command is `brew install gnu-sed` to install gnu sed.
SEDCMD := sed
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Darwin)
	SEDCMD := gsed
endif


all: lint clean

# Run any lints
lint: yamllint

yamllint:
	# This runs yamllint against everything yaml in this repo, it will exitcode !0 if it fails
	yamllint -c .yamllint.yaml ./

clean:
	# This strips trailing spaces
	find  ./ \( -iname "*.yaml" -o -iname "*.yml" \) -exec ${SEDCMD} -i 's/[[:space:]]*$$//' {} \;
	# Todo add others?

setup:
	# Update our helm subchart...
	helm dependencies update deployment/${SERVICE_NAME}

diff:
	helm diff upgrade --namespace ${K8S_NAMESPACE} --allow-unreleased ${CURRENT_HELM_CHART} deployment/${HELM_CHART}     -f deployment/${CURRENT_HELM_CHART}/values.yaml     -f deployment/${CURRENT_HELM_CHART}/values-${CI_ENVIRONMENT_SLUG}.yaml        --set global.namespace="${K8S_NAMESPACE}"

deploy:
	helm upgrade --namespace ${K8S_NAMESPACE} --install ${CURRENT_HELM_CHART} deployment/${HELM_CHART}     -f deployment/${CURRENT_HELM_CHART}/values.yaml     -f deployment/${CURRENT_HELM_CHART}/values-${CI_ENVIRONMENT_SLUG}.yaml        --set global.namespace="${K8S_NAMESPACE}"
