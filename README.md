# Desafio DevSecOps — Gerenciador de Tarefas

## Sobre o Projeto
Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech.
Você receberá este projeto com vulnerabilidades propositais e uma pipeline incompleta.
Seu objetivo é **implementar a pipeline de segurança** e **corrigir as vulnerabilidades**.

## Estado atual
A pipeline executa verificações de segurança, assina o artefato e publica no GitHub Pages somente após os gates passarem.

## Sua missão
1. Implementar os steps de segurança no `pipeline.yml`
2. Fazer a pipeline **quebrar** ao detectar os problemas
3. Corrigir as vulnerabilidades encontradas
4. Fazer a pipeline **passar** com tudo verde ✅
5. Documentar o funcionamento da pipeline neste README

## O que implementar
- [x] Secrets Scanning com **Gitleaks**
- [x] SAST com **Semgrep**
- [x] SCA com **Grype**
- [x] Assinatura do artefato com Cosign
- [x] Deploy com **GitHub Pages**

## Como a pipeline funciona
No push para `main`, o GitHub Actions verifica o código com Gitleaks, Semgrep e Grype. Gitleaks procura credenciais expostas; Semgrep identifica padrões de código inseguros; e Grype detecta vulnerabilidades conhecidas nas dependências. Achados bloqueantes fazem o job falhar e impedem o deploy.

Se os gates passarem, a pipeline empacota o site, calcula seu hash e assina o artefato com Cosign usando a identidade OIDC do GitHub. O job de deploy verifica a assinatura antes de publicar no GitHub Pages.

**Atenção:** `API_KEY` e `DB_PASSWORD` são injetados no JavaScript do navegador neste exemplo. Portanto, ficam visíveis aos visitantes e não devem ser credenciais reais.

## URL de Produção
[Abrir aplicação no GitHub Pages](https://andrehs91.github.io/projeto-devsecop-desafio/)
