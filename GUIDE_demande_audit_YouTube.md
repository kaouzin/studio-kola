# Demande de validation YouTube (audit API) – Studio Kola

But : que les vidéos envoyées par le pipeline puissent être **publiées directement en public**
(aujourd'hui YouTube les force en privé car l'appli « Studio Kola » n'est pas auditée).

---

## Étape 0 – À faire TOUT DE SUITE (2 min) : passer l'appli en « Production »

Tant que l'appli est en mode « Test », Google fait **expirer l'accès YouTube au bout de 7 jours** :
la vidéo automatique tomberait en panne chaque semaine.

1. Ouvre https://console.cloud.google.com/auth/audience?project=gen-lang-client-0449114912
2. Section « État de publication » : clique **« Publier l'application »** → Confirmer.
   (Pas besoin de vérification Google pour un usage personnel ; l'écran « appli non validée »
   restera visible à la connexion, c'est normal.)
3. Préviens Claude : il relancera la connexion YouTube une fois (2 clics, comme la première fois).

## Étape 1 – Mettre en ligne la politique de confidentialité et les conditions (10 min)

YouTube exige deux pages publiques. Elles sont prêtes dans ce dossier :
- `politique_de_confidentialite.html`
- `conditions_utilisation.html`

Le plus simple et gratuit : **Google Sites** (avec ton compte Google)
1. https://sites.google.com → « Site vierge ». Titre : **Studio Kola**.
2. Page 1 « Privacy Policy » : ouvre `politique_de_confidentialite.html` dans ton navigateur,
   copie tout le texte, colle-le dans la page.
3. Ajoute une page « Terms of Service » (Pages → +) avec le texte de `conditions_utilisation.html`.
4. **Publier** (en haut à droite), adresse par ex. `studio-kola`.
5. Note les deux liens, du type :
   - https://sites.google.com/view/studio-kola/privacy-policy
   - https://sites.google.com/view/studio-kola/terms-of-service
6. Dans la console Google : https://console.cloud.google.com/auth/branding?project=gen-lang-client-0449114912
   → renseigne « Lien vers les règles de confidentialité » et « Lien vers les conditions d'utilisation » → Enregistrer.

## Étape 2 – Enregistrer une courte vidéo de démonstration (5 min)

YouTube veut voir comment l'outil utilise l'API. Avec l'**Outil Capture d'écran** de Windows
(touche Windows + Maj + R → mode vidéo), enregistre 1 à 2 minutes :
1. Le dossier `C:\Studio\pipeline` et une vidéo terminée (`final.mp4`).
2. La connexion : fenêtre PowerShell, `cd C:\Studio\pipeline` puis `python run.py auth youtube`,
   l'écran d'autorisation Google (scopes « Gérer vos vidéos » / « Afficher votre compte »).
3. L'envoi : la vidéo apparaissant dans YouTube Studio (onglet Shorts) avec la mention IA.
Mets la vidéo sur YouTube **en non répertoriée** (ou sur Google Drive en partage par lien) et garde le lien.

## Étape 3 – Remplir le formulaire

Formulaire : **https://support.google.com/youtube/contact/yt_api_form**
→ choisir **« YouTube API Services – Audit and Quota Extension Form »**.
Réponses à copier-coller (en anglais, c'est la langue attendue) :

| Champ | Réponse |
|---|---|
| Name / Email | Kola Konipo – kola.konipo@gmail.com |
| Organization | Individual creator (no company) – channel “ANKA MALIBA” |
| Channel URL | https://www.youtube.com/@ankamaliba223 (channel ID UCUZVnZelrudh4aHuRnN8cpw) |
| Google Cloud project number | **386313765262** |
| Project ID | gen-lang-client-0449114912 |
| OAuth client ID | 386313765262-50ithnmn04sbp7asl3ssfl1flc4sj5ps.apps.googleusercontent.com |
| API client name | Studio Kola |
| Type of request | Audit (to lift the private-only restriction on uploads). No quota increase needed. |
| Is the client for internal use only? | Yes – used only by me, on my own computer, for my own channel. |
| Number of users | 1 |
| Privacy policy URL | (lien Google Sites de l'étape 1) |
| Terms of service URL | (lien Google Sites de l'étape 1) |
| Demo / screencast URL | (lien de l'étape 2) |
| APIs / scopes used | YouTube Data API v3 – videos.insert (youtube.upload), channels.list mine=true (youtube.readonly) |

**Description of the API client (copier-coller) :**

> Studio Kola is a private desktop tool (Python script running on my own Windows PC) that I use to
> publish my own videos to my own YouTube channel “ANKA MALIBA”. I am the only user.
> Each day it produces one original short educational video about personal finance (script, AI-generated
> illustrations, voice-over, editing) and uploads it with videos.insert (resumable upload), setting the
> title, description, tags, category (Education), language, privacy status and the
> containsSyntheticMedia flag, since the videos are made with the help of AI. The description of every
> video also discloses the use of AI and lists the sources of the figures quoted.
> channels.list (mine=true) is only used to display which channel is connected after authorization.
> The tool does not read, store or process any data about other users, comments, subscribers or viewers.
> The OAuth token is stored only on my computer and never shared. I request the audit so that my uploads
> are no longer restricted to private mode and can be published publicly on my channel.

**Expected usage :** 1 upload per day (~1,700 quota units/day), well within the default 10,000 units.

## Ensuite

- Délai habituel : de quelques jours à quelques semaines. YouTube peut poser des questions par e-mail
  (réponds simplement, ou transmets-les à Claude).
- Une fois l'audit validé : Claude passe `privacy: public` dans `config.yaml` et les vidéos
  seront publiées directement en public à 16 h (heure de Paris).
- En attendant, rien ne change : vidéo envoyée en privé à 16 h, tu la passes en public vers 18 h.
