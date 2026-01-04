# 🐉 Guide : Retroport Mount WoW WotLK

## 📦 PARTIE 1 : MODELING

### 1️⃣ Extraction
🔹 **WoW.Export** → Choisis ton modèle → Télécharge **M2** + textures

### 2️⃣ Fix des Textures
🔧 **M2Mod** → Tools → **TXID Fix** → Charge le M2 → **Fix**

### 3️⃣ Conversion M2 → M2i
🔄 **M2Mod** → M2 → M2i → **GO!**

### 4️⃣ Réduction des Polygones (si Tris > 21,500)
📐 **Blender** → Importe le M2i  
📐 Sélectionne chaque mesh → Ajoute **Decimate**  
📐 Ajuste jusqu'à **Tris < 21,500**  
📐 **Applique** sur chaque mesh → Exporte M2i

### 5️⃣ Reconversion M2i → M2
🔄 **M2Mod** → M2i → M2 → **Preload** → **GO!**

### 6️⃣ Nettoyage des Skins
📂 Dossier **Export** → Renomme les `.skin` en supprimant `_lod`  
📂 Exemple : `mount_lod01.skin` → `mount01.skin`  
📂 Copie tout dans ton dossier "Creature" et supprime les anciens skins

### 7️⃣ Édition 010 Editor
🛠️ Ouvre le **M2** dans **010 Editor**  
🛠️ Template **M2.bt** → Va dans **nViews** → Change par le nombre de skins → **Save**

### 8️⃣ Conversion finale
✨ Tous les fichiers (M2 + skins) → **MultiConverter** → **Convert**

---

## 🗃️ PARTIE 2 : DBC

### 9️⃣ Créer les entrées DBC
📋 **WDBX Editor** :

**A) CreatureModelData.dbc**  
🔹 Duplique une ligne → Change **ID** (ex: 76000) + **ModelPath** vers ton modèle + Ajoute les textures dans **TextureVariation**

**B) CreatureDisplayInfo.dbc**  
🔹 Duplique Ashes of Al'ar (18545) → Change **ID** (ex: 50002) + **ModelID** (ex: 76000)

### 🔟 Créer Patch Creatures
📦 **MPQ Editor** → Nouveau : **patch-C.mpq** (Creature)  
📦 Structure : `DBFilesClient\` → Ajoute les DBCs  
📦 Ajoute aussi ton dossier **Creature** (M2 + textures)  
📦 Sauvegarde dans `WoW\Data\`

🔄 Copie les DBCs dans **client** (`DBFilesClient\`) et **serveur** (`dbc\`)

---

## 💾 PARTIE 3 : BASE DE DONNÉES

### 1️⃣1️⃣ HeidiSQL
🔹 **creature_model_info** → Duplique une ligne → Change **DisplayID** (76000)  
🔹 **item_template** → Duplique Ashes of Al'ar → Change **entry** (65000) + **spellid_1** (500001)

---

## 🎁 PARTIE 4 : ITEM & SPELL

### 1️⃣2️⃣ Spell.dbc
🔮 Duplique spell **40192** (Ashes of Al'ar)  
🔮 Change : **ID** (ex: 500001) + **EffectMiscValue_1** (ton DisplayID) (76000)

### 1️⃣3️⃣ Item.dbc
🎒 Duplique item **32458** (Ashes of Al'ar)  
🎒 Change : **ID** (ex: 65000) + **DisplayInfoID** = ICONE

### 1️⃣4️⃣ Créer Patch Spell
📦 Nouveau : **patch-S.mpq** (Spell)  
📦 `DBFilesClient\` → Ajoute **Spell.dbc** + **Item.dbc**  
📦 Sauvegarde dans `WoW\Data\`

🔄 Copie dans **client ET serveur** !

---

## 🎉 TESTER !

✅ Redémarre le serveur  
✅ Supprime `WoW\Cache`  
✅ En jeu : `.additem 65000`  
✅ Utilise l'item → **VOLE SUR TON DRAGON !** 🐉✨

---

**Bravo ! 🎊**
