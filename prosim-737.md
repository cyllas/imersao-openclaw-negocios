# ProSim737 - ProSim Aviation Research

## Visao Geral

O **ProSim737** e uma suite profissional de software de simulacao de voo desenvolvida pela **ProSim Aviation Research (ProSim-AR)**, empresa sediada na **Holanda**. E uma solucao completa para operacao de simuladores de voo do Boeing 737.

---

## Informacoes Gerais

### Caracteristicas Principais

| Aspecto | Detalhes |
|---------|----------|
| **Tipo** | Suite de avionicos e sistemas para simulador Boeing 737 |
| **Desenvolvedor** | ProSim Aviation Research (ProSim-AR) |
| **Sede** | Holanda |
| **Publico** | Entusiastas (home cockpit) e uso comercial/profissional |
| **Compatibilidade** | Microsoft Flight Simulator X (FSX), Prepar3D (P3D), X-Plane |
| **Arquitetura** | Modular - pode rodar em um ou multiplos computadores |

### Funcionalidades

1. **Simulacao de Sistemas de Aeronave:**
   - Hidraulica, pneumatica (bleed air), eletrico, combustivel
   - Flight Management System (FMS)
   - Autopilot
   - Displays de cockpit (PFD, ND, EICAS, etc.)

2. **Realismo:**
   - Mais de **200 malfunctions (falhas)** modeladas
   - Modelo de voo sofisticado e realista
   - Diferentes layouts de display

3. **Funcionalidade de Instrutor:**
   - Extensas opcoes para operador/instrutor
   - Controle de cenarios de treinamento

4. **Compatibilidade de Hardware:**
   - Compativel com todos os componentes de hardware de cockpit replica
   - Interface grafica para configuracao facil

### Modulos do Software

| Modulo | Descricao |
|--------|-----------|
| **ProSim737 System** | Logica central dos sistemas |
| **ProSim737 MCP** | Mode Control Panel |
| **ProSim737 Display** | Renderizacao dos instrumentos |
| **ProSim737 CDU** | Control Display Unit (FMC) |
| **ProSim737 Audio** | Sistema de audio |
| **ProSim737 Panel** | Controle de paineis |
| **ProSim737 Hardware Connector** | Interface com hardware fisico |

### Precos (Referencia)

| Licenca | Valor |
|---------|-------|
| **Licenca nao-comercial** | EUR 1.250 |
| **Assinatura de atualizacoes** | EUR 99/ano (opcional) |

### Ecossistema

A ProSim-AR tambem oferece:
- **ProSimA320** - Suite para Airbus A320
- **ProSim Training Solutions** (prosim.aero) - Solucoes para treinamento comercial de pilotos

---

## Detalhes Tecnicos

### Linguagem e Framework

| Aspecto | Tecnologia |
|---------|------------|
| **Plataforma** | Microsoft **.NET Framework** |
| **Versao .NET Requerida** | **.NET Framework 4.6** (minimo) |
| **Linguagem** | **C#** ou VB.NET (managed code) |
| **Tipo de Aplicacao** | Windows Desktop Applications (.NET) |
| **Runtime Adicional** | VC++ Redistributables (32/64 bits) - componentes nativos |

### Arquitetura de Comunicacao

| Componente | Tecnologia |
|------------|------------|
| **Comunicacao Inter-Modulos** | Protocolo de rede proprietario (TCP/IP) |
| **API Externa** | HTTP Web Server interno com **XML Gateway** |
| **Formato de Dados** | **XML** (configuracoes, dados, queries) |
| **Formato de API** | REST-like via HTTP |

### Interface de Integracao (API)

O ProSim737 expoe um **web server interno** para desenvolvimento de add-ons:

```
Endpoint: http://localhost:8080/xml?query=<action>&parameter=value
```

**Response Format (XML):**

```xml
<root>
  <query>[copy of query]</query>
  <success>[true/false]</success>
  <answer>
    [response data]
  </answer>
</root>
```

**Queries Disponiveis:**

| Query | Descricao |
|-------|-----------|
| `fms` | Dados do Flight Management System |
| `aircraft` | Parametros basicos da aeronave |
| `failures` | Lista de falhas suportadas |
| `armedFailures` | Sistema de falhas programadas |
| `groundPower` | Controle de energia de solo |
| `loadsheet` | Dados para folha de carga |
| `acars` | Uplink/downlink de mensagens ACARS |

### Exemplos de API

**Trigger failure f108 acima de 80kts:**
```
http://localhost:8080/xml?query=armedFailures&failures=f108&ias=80
```

**Remover failure numero 0:**
```
http://localhost:8080/xml?query=armedFailures&remove=0
```

**Query loadsheet:**
```
http://localhost:8080/xml?query=loadsheet
```

**ACARS uplink:**
```
http://localhost:8080/xml?query=acars&message=metar+response&content=metar+data
```

### Integracao com Simuladores

| Interface | Tecnologia |
|-----------|------------|
| **FSX/P3D** | **SimConnect SDK** (managed code - C#/.NET) |
| **X-Plane** | Plugin nativo (ProSim737 Plugin for X-Plane) |
| **Middleware** | **FSUIPC** (interface de hardware/software) |

### Requisitos de Sistema

#### Sistema Operacional
- Windows Vista (minimo)
- Windows 7, 8, 10 (recomendado)
- Ultimas atualizacoes do Windows instaladas

#### Dependencias de Software
- Microsoft .NET Framework 4.6+
- VC++ Redistributables (32 e 64 bits)
- FSUIPC (versao registrada)
- SimConnect RTM (para P3D)

#### Hardware Recomendado
- **ProSim737 System**: Processador quad-core rapido (i7 recomendado, uso de CPU < 2%)
- **ProSim737 Display**: Modulo mais exigente - usa CPU para renderizacao (sem aceleracao GPU)

### Caracteristicas de Desenvolvimento

1. **Modular**: Cada modulo e uma aplicacao .NET separada
2. **Distribuido**: Modulos podem rodar em maquinas diferentes via rede
3. **Extensivel**: API XML permite desenvolvimento de add-ons customizados
4. **Renderizacao**: ProSim737 Display **nao usa aceleracao de GPU** - renderizacao via CPU (software rendering)

### Evidencias da Stack .NET/C#

1. Requer instalacao explicita do .NET Framework 4.6
2. Manual antigo (2012) menciona: *"All ProSim737 modules are DotNet Windows applications"*
3. Projetos de terceiros no GitHub relacionados ao ProSim737 (ex: HoppieAcarsClient) sao desenvolvidos em **C#**
4. Uso de SimConnect managed API (exclusiva para C#/VB.NET)
5. Arquivos de configuracao em XML (padrao comum em aplicacoes .NET)

---

## Recursos e Links

| Recurso | URL |
|---------|-----|
| **Site Oficial** | https://prosim-ar.com/ |
| **ProSim737 Home** | https://prosim-ar.com/prosim-737/ |
| **Wiki/Manual** | https://wiki.prosim-ar.com/ |
| **Downloads** | http://prosim-ar.com/downloads/ |
| **ProSim Training Solutions** | https://prosim.aero/ |

---

## Resumo Tecnico

O **ProSim737** e desenvolvido em **C# (.NET Framework)**, com uma arquitetura modular cliente-servidor usando **TCP/IP** para comunicacao interna e **HTTP/XML** para API externa. A escolha do .NET permite integracao nativa com o **SimConnect SDK** da Microsoft e facilita o desenvolvimento de componentes distribuidos em multiplas maquinas Windows.

E considerado uma das opcoes mais completas e profissionais do mercado para quem quer construir um simulador de voo realista do Boeing 737 em casa ou para fins comerciais de treinamento.

---

## Documentacao Tecnica e SDK

### Disponibilidade de Codigo-Fonte

**Nao existe repositorio oficial open-source no GitHub** com o codigo-fonte do ProSim737. O software e **closed-source/proprietario**. Porem, existem recursos tecnicos importantes para integracao.

### ProSim SDK Oficial

| Item | Detalhes |
|------|----------|
| **URL** | https://download.prosim-ar.com/ProSimSDK/ |
| **Arquivo** | `ProSimSDK.zip` (64KB) |
| **Ultima Atualizacao** | 2023-05-10 |
| **Tipo** | DLL .NET para integracao |
| **Funcao** | Acesso programatico aos datarefs (variaveis do simulador) |

O SDK permite:
- Leitura/escrita de **datarefs** (variaveis de estado do simulador)
- Integracao com hardware externo
- Desenvolvimento de add-ons customizados

### Repositorios de Terceiros no GitHub

#### pyprosim (Python Wrapper)

| Item | Detalhes |
|------|----------|
| **URL** | https://github.com/lucasangarola/pyprosim |
| **Linguagem** | Python |
| **Dependencia** | pythonnet |
| **Funcao** | Wrapper para o ProSim SDK em Python |
| **Testado com** | ProSim B738 v3.29 |
| **Licenca** | MIT |

**Exemplo de uso:**

```python
# Instalacao
pip install pythonnet
pip install .  # no diretorio do pyprosim

# Uso basico
from pyprosim import ProSim

prosim = ProSim()
value = prosim.get_dataref("some_dataref_name")
prosim.set_dataref("some_dataref_name", new_value)
```

**Requisitos:**
- Python 3.11+
- pythonnet
- ProSim SDK DLL (inclusa no repositorio ou download oficial)

### Interfaces de Integracao Disponiveis

| Interface | Tipo | Uso |
|-----------|------|-----|
| **XML Gateway** | HTTP/REST-like | Add-ons, automacao, IOS customizado |
| **ProSim SDK** | DLL .NET | Integracao profunda, hardware externo |
| **Drivers** | Protocolo proprietario | SIOC, Phidgets, Bodnar, CPFlight, Saitek |

### Datarefs

**Datarefs** sao variaveis que representam o estado completo do simulador. Exemplos mencionados nas release notes:

- Airline data e aircraft tail number
- CDU screen content
- Calculated gross thrust
- SDK printer datarefs
- VOR/ADF bearing datarefs
- IRS heading datarefs

**Nota:** Nao existe lista completa de datarefs publicada oficialmente. A descoberta e feita via:
- Release notes (novos datarefs adicionados)
- Forum da comunidade
- Engenharia reversa do SDK

### Documentacao Oficial Disponivel

| Recurso | URL | Conteudo |
|---------|-----|----------|
| **Wiki/Manual Principal** | https://wiki.prosim-ar.com/index.php/ProSim737_Manual | Manual completo do usuario |
| **ProSim737 System** | https://wiki.prosim-ar.com/index.php/ProSim737_System | Modulo principal/servidor |
| **Configuracao** | https://wiki.prosim-ar.com/index.php/ProSim737_Configuration | Todas as opcoes de config |
| **Interface XML** | https://wiki.prosim-ar.com/index.php/Interfacing_with_ProSim737 | API XML Gateway |
| **Release Notes** | https://wiki.prosim-ar.com/index.php/Release_Notes_-_ProSim737 | Historico de versoes |
| **Datalink** | https://wiki.prosim-ar.com/index.php/Datalink | Sistema ACARS/Datalink |
| **Forum Oficial** | https://www.prosim-ar.com/forum | Suporte da comunidade |

### Recursos Nao-Oficiais da Comunidade

| Recurso | URL | Conteudo |
|---------|-----|----------|
| **SimObsession Reference** | https://www.simobsession.com/prosim737-reference/ | Referencia nao-oficial |
| **Release Notes Database** | https://www.simobsession.com/prosim737-reference/prosim-release-notes-database/ | Base de dados de releases |
| **Flaps2Approach** | https://www.flaps2approach.com/computers | Exemplo de arquitetura multi-PC |

### Arquitetura Multi-Computador (Exemplo)

Baseado em projetos da comunidade, uma configuracao tipica:

```
+------------------+     +------------------+     +------------------+
|    PC 1 (Server) |     |   PC 2 (Client)  |     |   PC 3 (Client)  |
+------------------+     +------------------+     +------------------+
| - Flight Sim     |     | - ProSim Display |     | - ProSim Display |
| - ProSim System  |<--->| - ProSim CDU     |<--->| - ProSim IOS     |
| - ProSim MCP     | TCP | - Navigraph      | TCP |                  |
+------------------+     +------------------+     +------------------+
```

**Comunicacao:** Todos os modulos se conectam ao ProSim System via TCP/IP usando o IP do servidor.

### Limitacoes da Documentacao

| Aspecto | Status |
|---------|--------|
| **Codigo-fonte** | Nao disponivel (closed-source) |
| **Lista completa de datarefs** | Nao publicada oficialmente |
| **Documentacao do SDK** | Limitada - depende de forum/comunidade |
| **Arquitetura interna** | Nao documentada publicamente |
| **Protocolo TCP interno** | Proprietario, nao documentado |

### Como Obter Mais Informacoes

1. **Forum Oficial** - Melhor fonte para duvidas tecnicas
2. **Contato direto com ProSim-AR** - Para licencas comerciais/profissionais
3. **Comunidade** - SimObsession, Flaps2Approach, forums de cockpit builders
4. **Engenharia reversa** - Projetos como pyprosim

---

## Sistema de Licenciamento

### Modelo de Licenciamento

| Aspecto | Detalhes |
|---------|----------|
| **Tipo** | Licenca por hardware (hardware-bound) |
| **Validacao** | Online via servidores ProSim-AR |
| **Chaves** | Product Key + Update Subscription Key |
| **Armazenamento Local** | Arquivos `.lic` em `C:\ProgramData\ProSim-AR\ProSimB738\` |

### Fluxo de Ativacao

```
+-------------------+     +----------------------+     +------------------+
|   Compra Online   | --> |  Email "Shipment"    | --> |  Product Key     |
|   (prosim-ar.com) |     |  (em ate 24h)        |     |  Update Key      |
+-------------------+     +----------------------+     +------------------+
                                                              |
                                                              v
+-------------------+     +----------------------+     +------------------+
|  Licenca Ativada  | <-- |  Validacao Online    | <-- |  ProSim System   |
|  (arquivo .lic)   |     |  (servidores ProSim) |     |  File > License  |
+-------------------+     +----------------------+     +------------------+
```

### Tipos de Chave

| Chave | Funcao |
|-------|--------|
| **Product Key** | Licenca principal do software (compra inicial) |
| **Update Subscription Key** | Acesso a atualizacoes por 12 meses (incremental) |

### Requisitos de Conexao

| Momento | Internet Necessaria |
|---------|---------------------|
| **Ativacao inicial** | **Obrigatoria** |
| **Uso normal** | Revalidacao a cada **30 dias** |
| **Apos 30 dias offline** | Software **nao inicia** |

### Vinculacao de Hardware (Hardware Binding)

O ProSim737 usa **vinculacao de hardware** para proteger a licenca:

- Licenca e vinculada ao hardware da maquina onde foi ativada
- **Nao e possivel** mover a licenca para outro computador automaticamente
- Para migrar: contato obrigatorio com **ProSim Support** para reativacao

### Arquivos de Licenca

| Item | Localizacao |
|------|-------------|
| **Arquivos .lic** | `C:\ProgramData\ProSim-AR\ProSimB738\` |
| **Config.xml** | Pasta de instalacao do ProSim737 System |

### Troubleshooting de Ativacao

Se houver erro de ativacao com licenca valida:

1. Executar ProSim com **direitos de administrador**
2. Verificar **acesso a internet** no PC com ProSim System
3. Verificar se **firewall** nao esta bloqueando
4. **Deletar todos os arquivos `*.lic`** na pasta do ProSim System
5. Reiniciar e re-inserir as chaves de licenca
6. Se persistir: contatar **ProSim Support**

### Opcoes de Avaliacao

| Tipo | Duracao | Requisito |
|------|---------|-----------|
| **Trial instantaneo** | 30 minutos | Nenhum (direto no software) |
| **Trial estendido** | 30 dias | Formulario + email |

### Transferencia de Licenca

Licencas **podem ser vendidas/transferidas**, mas com condicoes:

1. Licenca deve ter **subscription ativa** (nao expirada)
2. Proprietario atual solicita **ticket de transferencia**
3. Novo proprietario aceita **Terms & Conditions**
4. ProSim Support executa a transferencia
5. URL: https://prosim.atlassian.net/servicedesk/customer/portal/1/group/1/create/1

### Detalhes Tecnicos Inferidos

Com base no comportamento documentado, o sistema provavelmente usa:

| Componente | Tecnologia Provavel |
|------------|---------------------|
| **Identificacao de Hardware** | Hardware fingerprint (CPU ID, MAC address, etc.) |
| **Comunicacao** | HTTPS para servidores ProSim-AR |
| **Armazenamento** | Arquivo `.lic` (provavelmente criptografado/assinado) |
| **Validacao** | Token com expiracao de 30 dias |
| **Backend** | "DataServer" mencionado em forums |

### Resumo do Modelo de Licenciamento

O ProSim737 usa um modelo de **licenciamento online com validacao periodica**:

1. **Ativacao online obrigatoria** na primeira execucao
2. **Hardware binding** - licenca vinculada a maquina
3. **Revalidacao a cada 30 dias** via internet
4. **Arquivos .lic locais** armazenam o estado da licenca
5. **Migracao manual** - requer contato com suporte

Este modelo e comum em software comercial de nicho, equilibrando protecao contra pirataria com usabilidade para usuarios legitimos (permite uso offline por ate 30 dias).

---

## Analise de Seguranca - Sistema de Licenciamento

### Contexto de Ameacas

Existem **threads ativas em forums de pirataria** solicitando cracks do ProSim737, porem **sem evidencia de sucesso publico** ate o momento. Isso indica que o sistema de protecao atual tem alguma eficacia, mas ha interesse contínuo em quebra-lo.

### Vetores de Ataque Comuns em Aplicacoes .NET

#### 1. Decompilacao e Analise Estatica

| Ferramenta | Capacidade |
|------------|------------|
| **dnSpy** | Decompilacao + debugging + edicao de assemblies |
| **ILSpy** | Decompilacao open-source |
| **dotPeek** | Decompilacao (JetBrains) |
| **Reflector** | Decompilacao comercial |
| **ILDasm/ILAsm** | Desmontagem/remontagem de IL |

**Risco:** Codigo .NET compila para CIL (Common Intermediate Language), que e facilmente reversivel para codigo-fonte legivel.

#### 2. Tecnicas de Bypass Documentadas

**2.1 Byte Patching**
```
1. Identificar metodo de validacao (ex: CheckLicense())
2. Localizar instrucao condicional (brfalse/brtrue)
3. Modificar opcode para inverter logica ou sempre retornar true
4. Salvar assembly modificado
```

**2.2 Reflection Hijacking**
```csharp
// Tecnica documentada para hijack de LicenseManager
// Redireciona chamadas de validacao para metodo fake
VirtualProtect(targetMethod, size, PAGE_EXECUTE_READWRITE, out oldProtect);
Marshal.Copy(jumpToFake, 0, targetMethod, jumpToFake.Length);
```

**2.3 Hardware ID Spoofing**
```
- MAC Address: Facilmente alteravel via registro ou drivers
- CPU ID: Spoofers disponiveis
- Disk Serial: Modificavel via drivers
- Motherboard UUID: Alteravel em BIOS/UEFI
```

### Vulnerabilidades Potenciais do ProSim737

#### Baseado na Arquitetura Conhecida

| Componente | Vulnerabilidade Potencial | Risco |
|------------|---------------------------|-------|
| **.NET Framework** | Decompilacao trivial sem obfuscacao | ALTO |
| **Arquivos .lic** | Podem ser copiados/analisados | MEDIO |
| **Hardware binding** | MAC/CPU ID sao spoofaveis | MEDIO |
| **Validacao 30 dias** | Periodo offline permite analise | BAIXO |
| **Config.xml** | Dados em texto claro | BAIXO |

#### Locais Criticos para Analise

```
C:\ProgramData\ProSim-AR\ProSimB738\
├── *.lic                    # Arquivos de licenca
├── Config.xml               # Configuracao (possivel dados de licenca)
└── [outros arquivos]

[Pasta de instalacao]\
├── ProSim737System.exe      # Executavel principal
├── *.dll                    # Assemblies .NET (alvos de decompilacao)
└── ProSimSDK.dll            # SDK (pode conter logica de validacao)
```

#### Registro do Windows (Locais Provaveis)

```
HKEY_LOCAL_MACHINE\SOFTWARE\ProSim-AR\
HKEY_CURRENT_USER\SOFTWARE\ProSim-AR\
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\ProSim-AR\
```

### Analise do Modelo Atual

#### Pontos Fortes

| Aspecto | Eficacia |
|---------|----------|
| Validacao online obrigatoria | Dificulta uso offline permanente |
| Revalidacao a cada 30 dias | Limita janela de uso sem conexao |
| Hardware binding | Adiciona camada de protecao |
| Sem crack publico conhecido | Indica alguma robustez |

#### Pontos Fracos Potenciais

| Aspecto | Risco |
|---------|-------|
| .NET sem obfuscacao aparente | Decompilacao trivial |
| Hardware IDs spoofaveis | Bypass de binding |
| Arquivos .lic locais | Analise/copia possivel |
| SDK publico disponivel | Facilita engenharia reversa |

### Recomendacoes de Hardening

#### Nivel 1 - Essencial

| Medida | Implementacao |
|--------|---------------|
| **Obfuscacao forte** | Dotfuscator, ConfuserEx, SmartAssembly |
| **Anti-tampering** | Verificacao de integridade de assemblies |
| **Anti-debugging** | Deteccao de dnSpy, debuggers |
| **Code signing** | Strong naming + verificacao em runtime |

#### Nivel 2 - Avancado

| Medida | Implementacao |
|--------|---------------|
| **Hardware fingerprint robusto** | Combinar multiplos IDs + TPM se disponivel |
| **Criptografia de .lic** | AES-256 + assinatura RSA |
| **Validacao server-side critica** | Mover logica critica para servidor |
| **Packing** | Themida, VMProtect |

#### Nivel 3 - Arquitetural

| Medida | Implementacao |
|--------|---------------|
| **Thin client** | Funcionalidades criticas em servico web |
| **License server dedicado** | FlexLM, SafeNet |
| **Telemetria de uso** | Detectar padroes anomalos |
| **Watermarking** | Identificar origem de vazamentos |

### Ferramentas para Analise de Seguranca

#### Red Team (Teste de Penetracao)

| Ferramenta | Uso |
|------------|-----|
| **dnSpy** | Decompilacao e debugging |
| **de4dot** | Deobfuscacao |
| **Procmon** | Monitorar acessos a arquivos/registro |
| **Wireshark** | Analisar comunicacao com servidor |
| **API Monitor** | Interceptar chamadas de API |

#### Blue Team (Defesa)

| Ferramenta | Uso |
|------------|-----|
| **ConfuserEx** | Obfuscacao open-source |
| **Dotfuscator** | Obfuscacao comercial |
| **PEiD/Detect It Easy** | Verificar protecoes aplicadas |
| **YARA** | Criar signatures de cracks conhecidos |

### Proximos Passos Sugeridos

1. **Analise estatica** dos assemblies do ProSim737 com dnSpy para avaliar nivel de obfuscacao
2. **Monitoramento** de forums de pirataria para detectar vazamentos
3. **Teste de spoofing** de hardware IDs para validar robustez do binding
4. **Analise de trafego** entre cliente e servidor de licencas
5. **Auditoria** dos arquivos .lic para entender formato e criptografia

---

## Catalogo de Cyber Threat Intelligence

### Fontes de Ameacas Identificadas

#### Forums de Pirataria

| Plataforma | URL | Tipo | Status | Observacoes |
|------------|-----|------|--------|-------------|
| **SuprBay (PirateBay Forum)** | `https://pirates-forum.org/Thread-REQ-ProSim737-crack` | Forum | ATIVO | Requests desde 2018, sem crack confirmado |
| **SuprBay - ProSim A320** | `https://pirates-forum.org/Thread-REQ-PROSIM-A320-Suite` | Forum | ATIVO | Request para suite A320 |
| **SuprBay - ProSim Geral** | `https://pirates-forum.org/Thread-Prosim` | Forum | ATIVO | Thread generico sobre ProSim |
| **SuprBay - Flight Sim World** | `https://pirates-forum.org/Forum-Flight-Sim-World` | Forum | ATIVO | Secao dedicada a pirataria de flight sim |
| **Google Sites (SEO Poisoning)** | `https://sites.google.com/view/howtocrackprosim737` | Pagina | ATIVO | Possivel phishing/malware (requer login) |

#### Subreddits Relacionados

| Subreddit | URL | Tipo | Risco |
|-----------|-----|------|-------|
| **r/flightsim_pirate** | `https://www.reddit.com/r/flightsim_pirate/` | Subreddit | ALTO - Dedicado a pirataria de flight sim |
| **r/PiratedGames** | `https://www.reddit.com/r/PiratedGames/` | Subreddit | MEDIO - Geral, pode conter requests |

#### Marketplaces Secundarios

| Plataforma | URL | Tipo | Observacoes |
|------------|-----|------|-------------|
| **CockpitBuilders Classifieds** | `https://www.cockpitbuilders.com/` | Forum | Vendas de licencas usadas (legitimo mas monitorar) |

### Threads Especificos Catalogados

#### Thread Principal - SuprBay ProSim737 Crack

| Campo | Valor |
|-------|-------|
| **URL** | `https://pirates-forum.org/Thread-REQ-ProSim737-crack` |
| **Data Inicio** | 2018-07-18 |
| **Ultimo Post** | 2022-02-08 (baseado na pesquisa) |
| **Versoes Mencionadas** | v1.56, v2, v3 |
| **Status do Crack** | NAO ENCONTRADO |
| **Views** | Alto volume (indica interesse) |
| **Usuarios Ativos** | Multiplos, requests recorrentes |

#### Indicadores de Interesse por Versao

| Versao | Mencoes | Periodo |
|--------|---------|---------|
| v1.56 | Multiplas | 2018-2019 |
| v2.x | Multiplas | 2019-2020 |
| v3.x | Multiplas | 2020-2022 |

### Taticas, Tecnicas e Procedimentos (TTPs) Observados

#### Vetores de Distribuicao Potenciais

| Vetor | Descricao | Risco |
|-------|-----------|-------|
| **Torrent/Magnet** | Nenhum encontrado para ProSim737 | BAIXO |
| **Direct Download** | Nenhum site warez com ProSim737 identificado | BAIXO |
| **Keygen** | Nenhum keygen publico identificado | BAIXO |
| **License Sharing** | Possivel via forums privados | MEDIO |
| **SEO Poisoning** | Sites falsos (Google Sites) para phishing | MEDIO |

#### Padroes de Comportamento dos Atacantes

```
1. REQUEST em forum publico (SuprBay)
2. Mencao de alto custo como motivacao (EUR 1.250)
3. Mencao de trial limitado (30 min) como frustracao
4. Mencao de updates frequentes dificultando crack
5. Ausencia de respostas com solucoes funcionais
```

### Indicadores de Comprometimento (IOCs)

#### Hashes de Arquivos Suspeitos (a serem coletados)

| Tipo | Descricao | Hash |
|------|-----------|------|
| **Executaveis modificados** | A coletar durante analise | TBD |
| **DLLs patcheadas** | A coletar durante analise | TBD |
| **Arquivos .lic falsos** | A coletar durante analise | TBD |

#### Dominios/URLs Suspeitos

| URL | Tipo | Risco | Acao |
|-----|------|-------|------|
| `sites.google.com/view/howtocrackprosim737` | Phishing/SEO Poisoning | ALTO | Reportar ao Google |
| `pirates-forum.org/*prosim*` | Forum de pirataria | MEDIO | Monitorar |

#### Palavras-Chave para Monitoramento

```
prosim737 crack
prosim737 keygen
prosim737 license key free
prosim737 torrent
prosim737 bypass
prosim737 patch
prosim crack
prosim license generator
prosim serial
prosim activation bypass
```

### Inteligencia de Ameacas - Timeline

| Data | Evento | Fonte |
|------|--------|-------|
| 2018-07-18 | Primeiro request publico para crack ProSim737 | SuprBay |
| 2018-10-11 | Thread generico "Prosim" criado | SuprBay |
| 2020-05-04 | Request para compra de licenca usada | CockpitBuilders |
| 2022-02-08 | Ultimo post observado no thread de crack | SuprBay |
| 2025-04-29 | Pagina Google Sites "howtocrackprosim737" detectada | Google Sites |

### Analise de Gap de Seguranca

#### Por que nao existe crack publico?

| Fator | Impacto na Protecao |
|-------|---------------------|
| **Validacao online obrigatoria** | ALTO - Dificulta uso permanente offline |
| **Revalidacao a cada 30 dias** | ALTO - Limita utilidade de patches |
| **Nicho de mercado pequeno** | MEDIO - Menos interesse de grupos de cracking |
| **Preco alto** | BAIXO - Normalmente atrai mais crackers |
| **Updates frequentes** | ALTO - Invalida patches rapidamente |

### Recomendacoes de Monitoramento

#### Fontes para Vigilancia Continua

| Fonte | Frequencia | Metodo |
|-------|------------|--------|
| **SuprBay Flight Sim World** | Diario | Web scraping + alertas |
| **Reddit r/flightsim_pirate** | Diario | Reddit API + keywords |
| **Google Alerts** | Continuo | Keywords configuradas |
| **VirusTotal** | Semanal | Busca por samples ProSim |
| **GitHub** | Semanal | Busca por repos suspeitos |

#### Keywords para Alertas Automatizados

```
"prosim737" AND ("crack" OR "keygen" OR "serial" OR "patch" OR "bypass")
"prosim" AND ("license" OR "key") AND ("free" OR "generator")
"prosim-ar" AND ("hack" OR "crack")
```

### Contatos para Report de Abuso

| Plataforma | Tipo de Report | URL/Email |
|------------|----------------|-----------|
| **Google** | SEO Poisoning/Phishing | https://safebrowsing.google.com/safebrowsing/report_phish/ |
| **Reddit** | Pirataria | Report via interface do Reddit |
| **GitHub** | DMCA | https://github.com/contact/dmca |

### Status Geral de Ameacas

| Metrica | Valor | Tendencia |
|---------|-------|-----------|
| **Cracks publicos disponiveis** | 0 | Estavel |
| **Keygens disponiveis** | 0 | Estavel |
| **Nivel de interesse em forums** | MEDIO | Estavel |
| **Eficacia da protecao atual** | ALTA | Positiva |
| **Risco de vazamento futuro** | MEDIO | Monitorar |

---

## Analise Tecnica: Bypass via Registro do Windows

### Contexto da Inteligencia

Informacoes obtidas via OSINT e outras fontes de inteligencia indicam que atacantes estao explorando **manipulacao do registro do Windows** para bypass do sistema de licenciamento do ProSim737.

### Locais de Registro Comuns para Licenciamento .NET

#### Hierarquia Padrao

```
HKEY_LOCAL_MACHINE (HKLM)
└── SOFTWARE
    ├── [Nome do Fabricante]
    │   └── [Nome do Produto]
    │       ├── License
    │       ├── InstallDate
    │       ├── ExpirationDate
    │       └── TrialStart
    └── WOW6432Node (para apps 32-bit em Windows 64-bit)
        └── [Nome do Fabricante]
            └── [Nome do Produto]

HKEY_CURRENT_USER (HKCU)
└── SOFTWARE
    ├── [Nome do Fabricante]
    │   └── [Nome do Produto]
    └── Classes
        └── CLSID
            └── {GUID}  (alguns apps usam GUIDs para ofuscar)
```

#### Locais Provaveis do ProSim737

| Caminho de Registro | Probabilidade | Uso Provavel |
|---------------------|---------------|--------------|
| `HKLM\SOFTWARE\ProSim-AR\` | ALTA | Dados de licenca global |
| `HKLM\SOFTWARE\ProSim-AR\ProSim737\` | ALTA | Config especifica do produto |
| `HKCU\SOFTWARE\ProSim-AR\` | MEDIA | Dados por usuario |
| `HKLM\SOFTWARE\WOW6432Node\ProSim-AR\` | MEDIA | Se app 32-bit |
| `HKCU\SOFTWARE\Classes\CLSID\{GUID}` | BAIXA | Ofuscacao via GUID |

#### Valores de Registro Tipicos em Sistemas de Licenciamento

| Nome do Valor | Tipo | Conteudo Tipico |
|---------------|------|-----------------|
| `License` | REG_SZ / REG_BINARY | Chave de licenca (possivelmente criptografada) |
| `InstallDate` | REG_QWORD / REG_SZ | Timestamp da instalacao |
| `ExpirationDate` | REG_QWORD / REG_SZ | Data de expiracao |
| `TrialStart` | REG_QWORD | Inicio do periodo trial |
| `LastValidation` | REG_QWORD | Ultima validacao online |
| `HWID` | REG_SZ | Hardware fingerprint |
| `MachineGuid` | REG_SZ | Identificador da maquina |
| `ActivationStatus` | REG_DWORD | Status (0=trial, 1=ativo, 2=expirado) |

### Tecnicas de Bypass via Registro Documentadas

#### 1. Manipulacao de Timestamp

**Descricao:** Alterar timestamps armazenados para resetar periodo de trial.

```
Tecnica:
1. Localizar chave com InstallDate ou TrialStart
2. Modificar valor para data futura ou resetar para hoje
3. Reiniciar aplicacao

Ferramenta: RunAsDate (simula data/hora diferente)
```

**Exemplo de Bypass (StartAllBack - documentado publicamente):**
```
Caminho: HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\CLSID\{GUID}
Metodo: Modificar "Last Write Time" da chave de registro
Resultado: Reset do contador de trial
```

#### 2. Delecao de Chaves de Trial

**Descricao:** Remover completamente dados de trial para simular nova instalacao.

```
Tecnica:
1. Identificar chaves relacionadas ao produto em HKLM e HKCU
2. Exportar backup (.reg)
3. Deletar chaves identificadas
4. Limpar arquivos em %ProgramData% e %AppData%
5. Reinstalar ou executar aplicacao
```

**Locais a verificar:**
```
HKLM\SOFTWARE\[Vendor]\
HKCU\SOFTWARE\[Vendor]\
%ProgramData%\[Vendor]\
%AppData%\[Vendor]\
%LocalAppData%\[Vendor]\
```

#### 3. Modificacao de Valores de Licenca

**Descricao:** Alterar diretamente valores que controlam status da licenca.

```
Tecnica:
1. Usar Procmon para monitorar acessos ao registro durante validacao
2. Identificar valores lidos/escritos
3. Modificar valores para simular licenca valida

Valores alvo comuns:
- ActivationStatus: 0 -> 1
- IsLicensed: false -> true
- ExpirationDate: [data passada] -> [data futura]
- TrialDaysRemaining: 0 -> 30
```

#### 4. Spoofing de Hardware ID via Registro

**Descricao:** Modificar ou criar valores que simulam hardware diferente.

```
Locais de HWID no registro:
HKLM\SOFTWARE\Microsoft\Cryptography\MachineGuid
HKLM\SYSTEM\CurrentControlSet\Control\IDConfigDB\Hardware Profiles\0001\HwProfileGuid

Tecnica:
1. Extrair HWID de maquina licenciada
2. Modificar MachineGuid no registro da maquina alvo
3. Spoofar MAC address via Device Manager
4. Usar licenca "emprestada"
```

#### 5. Interceptacao de Chamadas de Registro

**Descricao:** Usar API hooking para interceptar e modificar chamadas ao registro.

```csharp
// Tecnica de hooking documentada
// Intercepta RegQueryValueEx para retornar valores falsos
[DllImport("kernel32.dll")]
static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, 
    uint flNewProtect, out uint lpflOldProtect);

// Redireciona chamadas de leitura de registro para retornar licenca valida
```

### Ferramentas Usadas em Ataques de Registro

| Ferramenta | Funcao | Uso no Ataque |
|------------|--------|---------------|
| **Procmon (SysInternals)** | Monitoramento de registro | Identificar chaves acessadas |
| **RegShot** | Comparacao de snapshots | Detectar mudancas apos instalacao |
| **Registry Explorer** | Analise forense | Examinar estrutura de chaves |
| **RunAsDate** | Virtualizacao de data/hora | Bypass de expiracao temporal |
| **API Monitor** | Interceptacao de API | Capturar chamadas de registro |
| **x64dbg/dnSpy** | Debugging | Identificar logica de validacao |

### Indicadores de Ataque via Registro (IOAs)

#### Padroes de Acesso Suspeitos

| Padrao | Indicador |
|--------|-----------|
| **Leitura massiva** | Multiplas leituras em HKLM\SOFTWARE\ProSim-AR em curto periodo |
| **Escrita em trial** | Modificacao de valores *Date* ou *Expiration* |
| **Delecao de chaves** | Remocao de subchaves de licenca |
| **Acesso a MachineGuid** | Leitura/escrita em chaves de HWID |

#### Eventos do Windows para Monitorar

```
Event ID 4657 - Registry value modified
Event ID 4656 - Handle to registry key requested
Event ID 4663 - Attempt to access registry key

Filtros recomendados:
- ObjectName contains "ProSim"
- ObjectName contains "License"
- ProcessName NOT in whitelist
```

### Analise de Vulnerabilidades Especificas

#### Vulnerabilidade 1: Timestamp em Texto Claro

| Campo | Valor |
|-------|-------|
| **Severidade** | ALTA |
| **Descricao** | Timestamps de trial/validacao armazenados sem criptografia |
| **Impacto** | Reset infinito de trial |
| **Mitigacao** | Criptografar timestamps + validacao server-side |

#### Vulnerabilidade 2: Hardware ID Spoofavel

| Campo | Valor |
|-------|-------|
| **Severidade** | MEDIA |
| **Descricao** | HWID baseado apenas em MachineGuid ou MAC address |
| **Impacto** | Compartilhamento de licenca entre maquinas |
| **Mitigacao** | Usar multiplos identificadores + TPM |

#### Vulnerabilidade 3: Ausencia de Integridade

| Campo | Valor |
|-------|-------|
| **Severidade** | ALTA |
| **Descricao** | Valores de registro sem assinatura digital |
| **Impacto** | Modificacao arbitraria de dados de licenca |
| **Mitigacao** | Assinar valores com RSA + verificar em runtime |

#### Vulnerabilidade 4: Validacao Local

| Campo | Valor |
|-------|-------|
| **Severidade** | MEDIA |
| **Descricao** | Logica de validacao executada localmente |
| **Impacto** | Bypass via patching de codigo |
| **Mitigacao** | Mover validacao critica para servidor |

### Recomendacoes de Hardening para Registro

#### Nivel 1 - Protecao Basica

| Medida | Implementacao |
|--------|---------------|
| **Criptografia de valores** | AES-256 para todos os dados sensiveis |
| **Ofuscacao de chaves** | Usar GUIDs ao inves de nomes obvios |
| **Checksums** | Hash SHA-256 dos valores para detectar tampering |
| **ACLs restritivas** | Limitar acesso de escrita as chaves |

#### Nivel 2 - Protecao Avancada

| Medida | Implementacao |
|--------|---------------|
| **Assinatura digital** | RSA-2048 para valores criticos |
| **Multiplos locais** | Redundancia em registro + arquivo + servidor |
| **Verificacao cruzada** | Comparar dados locais com servidor |
| **Anti-tampering** | Detectar modificacoes e invalidar licenca |

#### Nivel 3 - Protecao de Integridade

| Medida | Implementacao |
|--------|---------------|
| **Kernel driver** | Proteger chaves via driver de kernel |
| **Virtualizacao** | Usar ambiente virtualizado para dados sensiveis |
| **TPM binding** | Vincular a TPM para hardware trust |
| **Watchdog** | Servico que monitora integridade continuamente |

### Script de Auditoria de Registro (PowerShell)

```powershell
# Script para auditoria de chaves de registro do ProSim737
# USO: Executar como administrador

$paths = @(
    "HKLM:\SOFTWARE\ProSim-AR",
    "HKLM:\SOFTWARE\WOW6432Node\ProSim-AR",
    "HKCU:\SOFTWARE\ProSim-AR",
    "HKLM:\SOFTWARE\Microsoft\Cryptography"
)

Write-Host "=== Auditoria de Registro ProSim737 ===" -ForegroundColor Cyan

foreach ($path in $paths) {
    if (Test-Path $path) {
        Write-Host "`n[ENCONTRADO] $path" -ForegroundColor Yellow
        Get-ChildItem $path -Recurse -ErrorAction SilentlyContinue | ForEach-Object {
            Write-Host "  Subchave: $($_.Name)"
            $_.GetValueNames() | ForEach-Object {
                $value = (Get-ItemProperty -Path $path -Name $_ -ErrorAction SilentlyContinue).$_
                Write-Host "    $_  = $value" -ForegroundColor Gray
            }
        }
    } else {
        Write-Host "`n[NAO ENCONTRADO] $path" -ForegroundColor Red
    }
}

# Verificar MachineGuid
$machineGuid = (Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Cryptography" -Name "MachineGuid").MachineGuid
Write-Host "`n[INFO] MachineGuid: $machineGuid" -ForegroundColor Green

# Verificar arquivos de licenca
$licPath = "$env:ProgramData\ProSim-AR\ProSimB738"
if (Test-Path $licPath) {
    Write-Host "`n[ARQUIVOS] $licPath" -ForegroundColor Yellow
    Get-ChildItem $licPath -Filter "*.lic" | ForEach-Object {
        Write-Host "  $($_.Name) - $($_.Length) bytes - $($_.LastWriteTime)"
    }
}
```

### Proximos Passos de Investigacao

1. **Executar Procmon** durante inicializacao do ProSim737 para mapear todos os acessos ao registro
2. **Capturar snapshot** com RegShot antes/depois da ativacao
3. **Analisar arquivos .lic** para entender formato e relacao com registro
4. **Testar modificacao** de valores em ambiente isolado
5. **Documentar comportamento** quando valores sao alterados/deletados
6. **Implementar monitoramento** de eventos 4657/4656/4663 em producao
