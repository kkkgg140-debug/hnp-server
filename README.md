# HNP PROXY Server

Repositório do servidor de configuração do HNP PROXY (Free Fire 1.130.1 / 1.130.20, 32-bit).

## Arquivos

| Arquivo | Descrição |
|---|---|
| `version.json` | Configuração que o jogo baixa (gamevar com HeadShotDamageRatio=10.0) |
| `localconfig.json` | Modelo de configuração local (`{"verAddr":"...","fakeVersion":"1.130.1","resetGuest":true}`) |

URL pública (GitHub Pages): `https://kkkgg140-debug.github.io/hnp-server/version.json`

## Offsets HS Peito (libil2cpp.so MD5 a14eb5c64fe5ad2e7b09ad8954abc1b5)

| Método (classe) | Offset | Função |
|---|---|---|
| `COW.ProfileDataPunishSwitchConfig$$GetHeadShotRatioValue` | `0x50251B0` | Lê o multiplicador de dano de headshot |
| `COW.GameConfig$$get_ResetGuest` | `0x5A7F9B4` | Reseta guest (resetGuest do localconfig) |
| `COW.GameConfig$$get_ResetGuestBeforeLogin` | `0x5A7FA9C` | Reseta guest antes do login |
| `COW.GameModeSettingManager$$GetIsHeadShotOnly` | `0x5D6605C` | Verifica modo "só headshot" (sala custom) |
| `COW.GamePlay.Player$$IsInNoHeadShotState` | `0x6237174` | Checa estado sem headshot do jogador |
| `COW.GamePlay.PlayerAttributes$$get_HeadShotDamageDecreaseScale` | `0x7000164` | Escala de redução de dano HS (getter) |
| `COW.GamePlay.PlayerAttributes$$set_HeadShotDamageDecreaseScale` | `0x70001C0` | Escala de redução de dano HS (setter) |
| `COW.UGCPlayerRepItem$$get_UGCHeadshotDamageDecreaseScale` | `0x7DF784C` | Escala UGC (getter) |
| `COW.UGCPlayerRepItem$$set_UGCHeadshotDamageDecreaseScale` | `0x7DF7854` | Escala UGC (setter) |
| `COW.BigHeadDataConfig$$GetHeadShotDamageScale` | `0x4D41198` | Escala de dano do modo Big Head |
| `COW.UIModelMatch$$get_IsCustomRoomAndHeadShotOnly` | `0x4ED8314` | Flag sala custom + só headshot (getter) |
| `COW.UIModelMatch$$set_IsCustomRoomAndHeadShotOnly` | `0x4ED831C` | Flag sala custom + só headshot (setter) |
| `COW.HUD.UIHudNameEnemyController$$IsHeadShotCollider` | `0x5B52090` | Verifica colisor de headshot no HUD |
| `COW.UGCTrainingPlayerRepItem$$get_OnlyHeadshot` | `0x7E12188` | Flag "só headshot" do treino (getter) |
| `COW.UGCTrainingPlayerRepItem$$set_OnlyHeadshot` | `0x7E12190` | Flag "só headshot" do treino (setter) |
| `COW.CustomRoomPreviewSettingHelper$$IsDropPresetHeadShotOnlyEnabled` | `0x4868E68` | Preset de headshot na sala custom |

### Método principal do HS Peito

O offset **`0x50251B0`** (`GetHeadShotRatioValue`) é o mais importante: ele é quem lê o multiplicador de dano de headshot. O `version.json` define `HeadShotDamageRatio=10.0`, então todo tiro no peito passa a contar como headshot com dano multiplicado.

### Observação

Não existe `get_OnlyHeadshot`/`set_OnlyHeadshot` na `COW.PlayerRepItem` ou `COW.GameConfig` nesta versão — o único `OnlyHeadshot` está na classe de treinamento (`UGCTrainingPlayerRepItem`, `0x7E12188`/`0x7E12190`), que não afeta partidas normais.

## Como atualizar

Edite o `version.json` ou `localconfig.json`, commit e push na branch `main`. O GitHub Actions publica automaticamente no GitHub Pages em alguns minutos.
