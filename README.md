# bawang-content
Innehåll på https://datasektionen.se

# Hur fungerar vår hemsida? 🤔
Vår hemsida består av tre delar: [bawang](https://github.com/datasektionen/bawang), [taitan](https://github.com/datasektionen/taitan) och [bawang-content](https://github.com/datasektionen/bawang-content).

### bawang-content
Detta repo. Här skrivs allt innehåll i Markdown.

### taitan
Taitan parsar Markdown (allt innehåll i detta repo) och gör om det till JSON och HTML. Besök https://taitan.datasektionen.se för att se ett exempel. Vill man se hur taitan parsar andra sidor kan man exempelvis besöka https://taitan.datasektionen.se/organisation.

### bawang
Bawang är vår React-frontend som hämtar data från taitan och lägger in det i sina komponenter. Bawang hämtar alltså JSON med HTML och annan information och laddar in som innehåll.

## Varför?
På detta sätt kan innehållsändringar göras av vem som helst som har tillgång till detta repo. Ändringarna behöver inte deployas för att komma upp på hemsidan, taitan hämtar allt direkt från detta repo. Vill man däremot göra förändringar i React-frontenden måste sådant såklart deployas.

# Redigera innehåll ✍️
Klona, gaffla (forka) repot (eller redigera i webbläsaren), gör en ny branch och jobba på den. När du är färdig gör du en PR (pull request). Gäller ändringarna någon annan nämnds/projekts/funktionärs sida kan det vara bra att tagga dem så att de godkänner förändringarna.

Vi har stängt av commits direkt till master.

## Köra lokalt 

Repot har en `docker-compose`-fil som sköter all setup med `bawang` och `taitan`. Så om du vill redigera hemsidan lokalt och vill se dina ändringar innan du pushar så är det bara att installera `docker` och sedan köra
```bash
docker compose up
```
Därefter så kommer sidan vara tillgänglig på `localhost:8000`. Om du ändrar på en sida så är det bara att ladda om webbläsaren för att se dina ändringar.

## Innehåll som är känsligt under mottagningen 🕶️

Om någon del av en sida inte ska visas under mottagningen kan detta automatiskt döljas under mörkläggningen genom att sätta `{{ if .reception -}}` innan och `{{- end }}` efter. Till exempel:

```html
{{ if .reception -}}
    Något mycket mycket hemligt!
{{- end }}
```

Om texten istället för att gömmas helt ska bytas ut mot något annat kan man innan `end`-delen lägga till `{{- else -}}` och ersättningen, till exempel:

```html
Konglig Datasektionen har {{ if .reception -}} sedan 1983 haft en mottagning varje år! {{- else -}} aldrig haft någon mottagning. {{- end }}
```

Mer specifikt används det inbyggda templating-systemet i Go, som man kan läsa mer om [här](https://pkg.go.dev/text/template).

Om någon sida ska döljas helt under mörkläggningen kan man istället sätta `Sensitive = true` i sidans `meta.toml`.

# Översätt hemsidan 🇬🇧🇺🇸
*Egentligen* borde hela webbsidan vara tillgänglig på engelska,
men vi har ett problem i att vi inte översatt stora delar av den än.
Du får gärna översätta den engelska sidan, som finns under mappen `/en`.

En engelskspråkig webbsida är jätteviktig för att utbytesstudenter ska kunna ta del av innehållet. 
Tänk på att det är de som är målgruppen när du översätter. Kom också ihåg att alla detaljer inte 
måste komma med i översättningen, bara du får med det viktigaste så är redan det väldigt värdefullt!
