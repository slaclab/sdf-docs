# TODO make a new secret for sdf-docs and update this
SECRET_PATH=secret/tid/sdf-docs/certs
KUBECTL_DEPLOY_CONTEXT ?= 'sdf-docs'
ensure-context:
	if [ '$(shell kubectl config current-context)' != $(KUBECTL_DEPLOY_CONTEXT) ]; then echo "Configured deployment context incorrect; expecting $(KUBECTL_DEPLOY_CONTEXT)."; exit 1; fi

# TODO update with new secrets/certs for sdf-docs
secrets: 
	mkdir -p etc/.secrets
#	set -e; for i in ondemand-dev.key ondemand-dev.crt ondemand-dev.intermediates; do vault kv get --field=$$i $(SECRET_PATH) > etc/.secrets/$$i ; done

clean-secrets:
	rm -rf etc/.secrets
    
run-apply:
	kubectl apply -k .

run-kustomize:
	kubectl kustomize .

dump: secrets run-kustomize clean-secrets

apply: ensure-context secrets run-apply clean-secrets

diff: 
	kubectl diff -k .

