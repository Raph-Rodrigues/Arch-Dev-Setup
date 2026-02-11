# Git Workflow & Convenções

## Estrutura de Branches

- `main`: Código em produção (somente merges de `dev`)
- `dev`: Branch de desenvolvimento (integração de fases)
- `fase-N-*`: Branches de fases do projeto
- `feature/*`: Features individuais

## Convenções de Commit

Seguimos **Conventional Commits**:
```
<tipo>(<escopo>): <mensagem>

[corpo opcional]

[rodapé opcional]
```

### Tipos de Commit

- `feat`: Nova feature
- `fix`: Correção de bug
- `docs`: Documentação
- `style`: Formatação (não afeta código)
- `refactor`: Refatoração de código
- `perf`: Melhorias de performance
- `test`: Testes
- `chore`: Tarefas de manutenção
- `build`: Sistema de build
- `ci`: Integração contínua

### Exemplos
```bash
feat(hyprland): adiciona configuração modular de keybinds
fix(waybar): corrige módulo de bateria
docs(readme): atualiza instruções de instalação
style(rofi): formata arquivo de configuração
refactor(scripts): reorganiza estrutura de diretórios
chore(git): atualiza .gitignore
```

## Workflow de Features

### 1. Criar Feature Branch
```bash
# Sempre derivar da branch de fase correspondente
git checkout fase-1-estrutura-base
git checkout -b feature/hyprland-modular
```

### 2. Desenvolver
```bash
# Fazer commits frequentes e atômicos
git add config/hypr/hyprland.conf
git commit -m "feat(hyprland): cria arquivo de configuração principal"
```

### 3. Merge na Fase
```bash
# Voltar para a branch de fase
git checkout fase-1-estrutura-base

# Merge da feature (--no-ff para manter histórico)
git merge --no-ff feature/hyprland-modular

# Deletar branch da feature (opcional, mas recomendado)
git branch -d feature/hyprland-modular
```

### 4. Merge da Fase em Dev
```bash
# Quando a fase estiver completa
git checkout dev
git merge --no-ff fase-1-estrutura-base
```

### 5. Merge em Main (Final)
```bash
# Apenas quando TUDO estiver pronto
git checkout main
git merge --no-ff dev
git tag -a v1.0.0 -m "Release inicial"
```

## Boas Práticas

1. **Commits pequenos e focados**: Um commit = uma mudança lógica
2. **Mensagens descritivas**: Explique o "porquê", não apenas o "o quê"
3. **Testar antes de commitar**: Garanta que tudo funciona
4. **Não commitar secrets**: Use `.gitignore` para arquivos sensíveis
5. **Documentar mudanças grandes**: Use o corpo do commit para explicar

## Visualizando o Histórico
```bash
# Ver árvore de commits
git log --graph --oneline --all --decorate

# Ver diferenças entre branches
git diff dev..fase-1-estrutura-base
```
