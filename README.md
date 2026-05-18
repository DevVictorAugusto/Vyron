<div align="center">
  <img src="./Logo/LogoVyron.png" alt="Vyron Logo" width="220" />
  <h1>Vyron</h1>
  <p><strong>Extrai e estrutura a inteligência de uma empresa a partir das suas URLs.</strong></p>
  <p>
    De links dispersos (Instagram, site, Google Maps) para um perfil único,
    validado e com proveniência — pronto para campanhas de marketing e geração de sites.
  </p>
</div>

## Conceito do Projeto
O **Vyron** é um **extrator de inteligência de empresas**. Você informa as fontes
(URL do Instagram, site, Google Maps e/ou arquivos locais) e ele devolve um
`CompanyProfile` estruturado: identidade, contatos, presença online e conteúdo.

O Vyron **apenas extrai e organiza** os dados. A interpretação criativa
(persona, copy, estratégia, layout de site) fica para um agente/skill que
consome esse perfil — mantendo a extração determinística e reutilizável.

## Problema que o Vyron ataca
- Dados da empresa espalhados em várias fontes, sem consolidação
- Falta de uma "fonte única da verdade" sobre a empresa
- Retrabalho manual para juntar contato, identidade e conteúdo
- Geração de conteúdo com IA sem base factual confiável

## Como funciona
Pipeline em `core/pipeline.py`:

1. **Coleta** — um collector por fonte (site, Instagram, Google Maps, arquivos locais)
2. **Extração** — contatos, cores reais da logo e conteúdo textual
3. **Merge** — consolida campos entre fontes, com confiança e proveniência
4. **Validação** — avalia completude e qualidade do perfil extraído
5. **Exportação** — `company_profile.json` + `extraction_report.json` por execução

## Saída
Cada execução é isolada em `outputs/runs/<empresa>/<run-id>/`:

| Arquivo | Conteúdo |
|---|---|
| `company_profile.json` | Perfil canônico da empresa |
| `extraction_report.json` | Score de completude, lacunas e avisos |
| `raw_sources.json` | Dump cru de cada fonte coletada |
| `events.jsonl` | Trilha rastreável da execução |

## Como iniciar
Requer Python 3.10+.

```bash
# 1. Instalar dependências (opcional — só habilita extração de cores da logo)
pip install -r requirements.txt

# 2. Iniciar a interface web
python webapp/server.py
```

Depois abra **http://127.0.0.1:8000** no navegador, informe as URLs da empresa
e clique em **Extrair inteligência**. O resultado aparece como um grafo de nós
e conexões (estilo "cérebro"), com download da imagem e do JSON do perfil.

Para usar outra porta: `python webapp/server.py --port 9000`

### Uso via linha de comando (sem interface)
```bash
# A partir de um JSON de entrada
python apps/run_extraction.py --input examples/input_example.json

# Modo interativo (perguntas no terminal)
python apps/run_extraction.py
```

### Testes
```bash
python -m unittest discover -s tests
```

## Diferencial
- Foco em **dados factuais** com **proveniência por campo**
- Consolidação real entre fontes (entity resolution)
- Saída estruturada e **reutilizável** por qualquer agente downstream
- Execuções isoladas e rastreáveis

## Status
Projeto em evolução (MVP funcional). Foco atual: robustez dos collectors e
cobertura do schema do perfil.

## Contato
Aberto para trocar ideia sobre Context Engineering, automação e produtos com IA.
