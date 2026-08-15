# Portal RAC — Regional Administrativa de Campinas

Portal de comunicação e gestão dos 22 Grupos de Trabalho da RAC (Congregação Cristã no Brasil).
Mural de comunicados, calendário de reuniões, diretório de membros, biblioteca de materiais e o
espaço de trabalho da Coordenação Geral — tudo num único arquivo (`index.html`), sem backend
próprio, salvando os dados no Firebase (Firestore).

## Como abrir

Publicado via GitHub Pages neste mesmo repositório. Acesse pelo link do Pages (Settings → Pages),
ou abra o `index.html` direto no navegador para testar localmente.

## Acesso

- **Consulta**: livre, sem login.
- **Publicar/editar**: exige um código de acesso por grupo de trabalho ou área, informado
  pessoalmente pelo Coordenador da Regional a cada responsável. Botão "Entrar como coordenador"
  no topo do Portal.

## Estrutura de dados (Firebase)

O Portal guarda tudo no Firestore, projeto `portal-rac-e2748`, numa única coleção `portal` com
um documento por tipo de dado (`rac_comunicados`, `rac_calendario`, `rac_tarefas`, `rac_membros`,
`rac_reunioes`, `rac_pauta`) — cada um com um campo `value` contendo o array em JSON.

As credenciais do projeto ficam no topo do `<script>` do `index.html`, na constante
`FIREBASE_CONFIG`. Se o projeto Firebase for recriado ou as chaves rotacionadas, é só atualizar
esses 6 valores ali.

### Regras do Firestore em uso

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /portal/{doc} {
      allow read, write: if true;
    }
  }
}
```

Sem autenticação real — a proteção é o código de acesso, distribuído com cuidado pelo Coordenador
da Regional, não uma senha de banco de dados. Se no futuro for necessário login individual por
pessoa, essas regras (e a lógica de acesso do Portal) precisam ser refeitas.

## Manutenção

Mudanças estruturais (layout, novas páginas, novos códigos de acesso, novos grupos de trabalho)
não são feitas pelos coordenadores — só editando o `index.html` diretamente.

Um guia de uso completo (para os coordenadores, sem detalhe técnico) está disponível separadamente
como documento Word: *Portal RAC — Guia de Uso*.
