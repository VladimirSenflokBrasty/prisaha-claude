# Claude: plugin, připojení a skilly

Claude (claude.ai, Desktop, Cowork, mobil, Claude Code) pracuje se stejnou aplikací, stejným MCP a stejnými skilly jako ChatGPT. Skilly jsou psané bez názvu klienta; v obou klientech vedou stejné postupy. Běh týmu a modelů zůstává výhradně na serveru aplikace.

## Co potřebujete

- Placený tarif Claude (Pro nebo vyšší).
- Svůj účet aplikace (heslo a TOTP nebo passkey). Přihlášení a souhlas probíhají pod ním; plugin ani skilly přístupové údaje neobsahují.

## Hlavní cesta: marketplace z veřejného repozitáře

1. V Claude otevřete **Customize → Plugins → Add → Add marketplace → Add from a repository** (česky Přizpůsobit → Pluginy → Přidat …) a vložte `VladimirSenflokBrasty/prisaha-claude`.
2. V seznamu zvolte **Přísaha — asistent** a **Add**.
3. Klikněte na **Connect**, přihlaste se účtem aplikace a v souhlasu povolte čtení i zadávání a úpravy (bez zápisu asistent nemůže zadávat práci týmu).
4. Ověřte: napište „Jaký mám tým?“. Claude má odpovědět jmény členů týmu.

Repozitář obsahuje jen plugin (popis, pět skillů, adresu MCP); žádná data ani kód aplikace. Vydává ho správce příkazem `make mcp-claude-marketplace-publish` spolu s balíčky.

Přihlášení hostovaného Claude probíhá zveřejněnou identitou Claude z povoleného seznamu; ruční Client ID není potřeba.

## Náhradní cesta: soubor `.zip`

Stránka **Propojení s AI** nabízí plugin jako soubor `.zip` (stejný obsah jako v marketplace). V Claude zvolte **Customize → Plugins → Add → Upload plugin**.

## Správce

- **Adresa MCP:** `<APP_URL>/mcp`.
- **Ruční vlastní konektor** (bez pluginu): **Customize → Connectors → Add custom connector**, zadejte adresu MCP. Client ID vyplňte v pokročilém nastavení jen tehdy, když volba „Use Claude's published identity“ selže; Client Secret nechte prázdný.
- **Jednotlivé skilly:** pokud verze Claude nabízí nahrání skillu, nahrajte ZIP každého skillu zvlášť (`prisaha-skill-<název>-….zip`). Obsahuje jen postup, bez připojení.

## Claude Code

Marketplace funguje i zde: `/plugin marketplace add VladimirSenflokBrasty/prisaha-claude`, potom `/plugin install prisaha-asistent@prisaha`. Dokumentace neslibuje, že `oauth` v `.mcp.json` uvnitř pluginu Claude Code respektuje, a jeho `localhost` s proměnným portem zveřejněná identita nepokrývá. Proto jednorázově přidejte připojení příkazem s Client ID a pevným portem (dosaďte skutečné hodnoty, najdete je v panelu **Pro správce**):

```sh
claude mcp add --transport http --client-id <CLIENT_ID> --callback-port 33418 prisaha <APP_URL>/mcp
```

Potom v Claude Code spusťte `/mcp`, zvolte `prisaha` a dokončete přihlášení v prohlížeči.

## Nácvik rozhovoru

V Claude je nácvik jen **textový**. Hlas s tímto konektorem v Claude není ověřený, proto jej aplikace ani skilly neslibují. Při zakládání nácviku v aplikaci zvolte klienta Claude; zadání se zkopíruje do chatu s připojeným konektorem, skill uloží přepis a hodnocení zpět do přípravy.

## Co je ověřeno a co ne

Formát marketplace a pluginu prověřil `claude plugin validate`. **Neověřeno** v této instalaci: skutečné přidání marketplace a nahrání `.zip` v Claude, přihlášení zveřejněnou identitou, chování `oauth` v `.mcp.json` v Claude Code a hlas v Claude. Neověřený krok vždy přiznejte, nepředpokládejte jej.

Plugin ani marketplace neobsahují heslo, token ani secret. Bez nakonfigurovaného Client ID správce Claude balíčky nevydává.
