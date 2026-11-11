# FIAP GitOps Repository

Este repositório contém as definições declarativas para deploy das aplicações FIAP usando GitOps.

## 🚀 Como usar

### ArgoCD
```bash
# Criar Application
kubectl apply -f applications/fiap-todo-api-app.yaml

# Sync via CLI
argocd app sync fiap-todo-api
```

### FluxCD
```bash
# Bootstrap
flux bootstrap github --owner=jefersonpapalinosp-sys --repository=fiap-dclt-aula04 --path=gitops-repo/clusters/production

# Aplicar configurações
kubectl apply -f clusters/production/
```

## 🔄 Workflow GitOps

1. **Desenvolvedor** faz mudança no código
2. **CI Pipeline** builda nova imagem
3. **Pipeline** atualiza tag no GitOps repo
4. **GitOps Agent** detecta mudança
5. **Deploy** automático no cluster

## 📊 Ambientes

- **Development**: Namespace `fiap-todo-dev`
- **Staging**: Namespace `fiap-todo-staging`  
- **Production**: Namespace `fiap-todo-prod`

## 🏷️ Convenções

### Tags de Imagem
- `v1.0.0` - Releases de produção
- `v1.0.0-rc.1` - Release candidates
- `dev-latest` - Desenvolvimento
- `staging-latest` - Staging

### Labels
- `app`: Nome da aplicação
- `version`: Versão da aplicação
- `environment`: Ambiente (dev/staging/prod)
- `managed-by`: Ferramenta GitOps (argocd/fluxcd)
