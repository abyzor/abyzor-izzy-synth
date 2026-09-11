# ABYZOR IZZY Synth — Changelog

## [v0.1.0] — 2026-09-10

Release inicial alinhada à versão embutida no build (`project(IZZY_SYNTH VERSION 0.1.0)` no CMake).

### Produto e build

- **ABYZOR IZZY Synth** — VST3 e Standalone Win64 (Release x64).
- Script [`build_vst.bat`](build_vst.bat): configure CMake (VS 2017 Win64), compila `IzzySynth_VST3` e `IzzySynth_Standalone`.
- Splash screen JUCE desligado no CMake.
- Artefatos: `build/IzzySynth_artefacts/Release/VST3/ABYZOR IZZY Synth.vst3` e `.../Standalone/ABYZOR IZZY Synth.exe`.

### Som e workflow

- Oito slots de patch; **GENERATE** preenche o próximo slot.
- Seletor de função: **BASS**, **STAB**, **LEAD**, **PLUCK**.
- Nove knobs de controle do patch (output, length, punch, space, etc.) ligados ao APVTS.

### Interface

- Logo ABYZOR no header (BinaryData).
- Scope de áudio e painel de slots.
- Teclado MIDI horizontal (range MIDI 24–84).
- Janela do editor ~900×732 px; barra **More from ABYZOR** acima do scope.

### Ecossistema ABYZOR

- Chips com link: **Genesis**, **Variations**, **One** (cores de marca, texto branco, larguras fixas).
- Chip **Updates**: verificação manual e automática (após ~3 s no standalone).

### Atualizações in-app

- `UpdateChecker` consulta o endpoint remoto e compara versão numérica com a do plugin instalado.
- Overlay com **Download** / **Later**; versão dispensada guardada no state do processor.

### Teclado do computador (QWERTY)

- Mapeamento padrão JUCE (`awsedftgyhujkolp;`).
- **Z** / **X** (sem modificadores): baixar / subir oitava de toque; scroll do teclado on-screen (`IzzyMidiKeyboard`).

---

## Versão de update (não é o changelog)

O plugin **não** lê este ficheiro. A versão instalada vem de `ABYZOR_VERSION_STRING` (CMake → **0.1.0**). O check de update faz GET em:

`https://abyzor.space/izzy/version.json`

Campos aceites para a versão remota (primeiro não vazio): `version`, `latest`, `latest_version`.  
URL de download: `downloadUrl`, `download`, `download_url` ou `url`; se faltar, usa `https://abyzor.space/products/izzy/`.

- Remoto **igual** a 0.1.0 → chip **Up to date**.
- Remoto **maior** que 0.1.0 → update disponível (ex.: `Up v0.2.0`).

### Exemplo para publicar no servidor

Ficheiro em `https://abyzor.space/izzy/version.json` (hospedagem no site; pode 404 até publicares):

```json
{
  "version": "0.1.0",
  "downloadUrl": "https://abyzor.space/products/izzy/"
}
```

Alternativa equivalente (também suportada pelo código):

```json
{
  "latest": "0.1.0",
  "url": "https://abyzor.space/products/izzy/"
}
```
