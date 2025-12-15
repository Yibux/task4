## Zadanie 1 (opcjonakne)
W celu zbudowania obrazu lokalnie, konieczna była zmiana `FROM openjdk:11-jdk-slim` -> `FROM eclipse-temurin:11-jre`, ponieważ nie mogło odnaleźć tego obrazu.

Skanowanie wykazało krytyczne luki bezpieczeństwa w zależnościach aplikacji Java (m.in. 8 podatności o statusie CRITICAL w bibliotekach Spring, H2 i Tomcat), które stanowią znacznie poważniejsze zagrożenie niż problemy wykryte w systemie operacyjnym kontenera (Ubuntu), gdzie dominują zagrożenia o niskim i średnim ryzyku.
![zad1_1](https://github.com/Yibux/task4/blob/main/zad1_1.png?raw=true)
![zad1_2](https://github.com/Yibux/task4/blob/main/zad1_2.png?raw=true)

## Zadanie 2 (opcjonalne)
Uruchomienie skanu semgrep dało następujące rezultaty:
```


┌─────────────┐
│ Scan Status │
└─────────────┘
  Scanning 1798 files tracked by git with 1063 Code rules:

  Language      Rules   Files          Origin      Rules
 ─────────────────────────────        ───────────────────
  <multilang>      62    1798          Community    1063
  js              156      13
  java            118      13
  html              1       8
  yaml             31       7
  json              4       6
  dockerfile        6       2
  ruby             72       1
  bash              4       1

Warning: 2 timeout error(s) in src/main/resources/static/vendors/bootstrap/js/bootstrap.bundle.js when running the
following rules: [javascript.aws-lambda.security.pg-sqli.pg-sqli, javascript.aws-lambda.security.tainted-html-
string.tainted-html-string]


┌──────────────────┐
│ 24 Code Findings │
└──────────────────┘

    Dockerfile
   ❯❯❱ dockerfile.security.missing-user-entrypoint.missing-user-entrypoint
          By not specifying a USER, a program in the container may run as 'root'. This is a security hazard.
          If an attacker can control a process running as root, they may have control over the container.
          Ensure that the last USER in a Dockerfile is a USER other than 'root'.
          Details: https://sg.run/k281

           ▶▶┆ Autofix ▶ USER non-root ENTRYPOINT ["java", "-jar", "/app.jar"]
           22┆ ENTRYPOINT ["java", "-jar", "/app.jar"]

    src/main/resources/static/vendors/bootstrap/js/bootstrap.bundle.js
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `configTypes` function argument, this might allow an attacker to cause a
          Regular Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main
          thread. For this reason, it is recommended to use hardcoded regexes instead. If your regex is run on
          user-controlled input, consider performing input validation or use a regex checking/sanitization
          library such as https://www.npmjs.com/package/recheck to verify that the regex does not appear
          vulnerable to ReDoS.
          Details: https://sg.run/gr65

          213┆ if (!new RegExp(expectedTypes).test(valueType)) {
            ⋮┆----------------------------------------
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `property` function argument, this might allow an attacker to cause a Regular
          Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main thread. For
          this reason, it is recommended to use hardcoded regexes instead. If your regex is run on user-
          controlled input, consider performing input validation or use a regex checking/sanitization library
          such as https://www.npmjs.com/package/recheck to verify that the regex does not appear vulnerable to
          ReDoS.
          Details: https://sg.run/gr65

          213┆ if (!new RegExp(expectedTypes).test(valueType)) {

   ❯❯❱ javascript.browser.security.insecure-document-method.insecure-document-method
          User controlled data in methods like `innerHTML`, `outerHTML` or `document.write` is an anti-pattern
          that can lead to XSS vulnerabilities
          Details: https://sg.run/LwA9

          5547┆ element.innerHTML = this._config.template;
            ⋮┆----------------------------------------
          5583┆ element.innerHTML = content;

    src/main/resources/static/vendors/bootstrap/js/bootstrap.esm.js
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `configTypes` function argument, this might allow an attacker to cause a
          Regular Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main
          thread. For this reason, it is recommended to use hardcoded regexes instead. If your regex is run on
          user-controlled input, consider performing input validation or use a regex checking/sanitization
          library such as https://www.npmjs.com/package/recheck to verify that the regex does not appear
          vulnerable to ReDoS.
          Details: https://sg.run/gr65

          209┆ if (!new RegExp(expectedTypes).test(valueType)) {
            ⋮┆----------------------------------------
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `property` function argument, this might allow an attacker to cause a Regular
          Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main thread. For
          this reason, it is recommended to use hardcoded regexes instead. If your regex is run on user-
          controlled input, consider performing input validation or use a regex checking/sanitization library
          such as https://www.npmjs.com/package/recheck to verify that the regex does not appear vulnerable to
          ReDoS.
          Details: https://sg.run/gr65

          209┆ if (!new RegExp(expectedTypes).test(valueType)) {

   ❯❯❱ javascript.browser.security.insecure-document-method.insecure-document-method
          User controlled data in methods like `innerHTML`, `outerHTML` or `document.write` is an anti-pattern
          that can lead to XSS vulnerabilities
          Details: https://sg.run/LwA9

          3789┆ element.innerHTML = this._config.template;
            ⋮┆----------------------------------------
          3825┆ element.innerHTML = content;

    src/main/resources/static/vendors/bootstrap/js/bootstrap.js
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `configTypes` function argument, this might allow an attacker to cause a
          Regular Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main
          thread. For this reason, it is recommended to use hardcoded regexes instead. If your regex is run on
          user-controlled input, consider performing input validation or use a regex checking/sanitization
          library such as https://www.npmjs.com/package/recheck to verify that the regex does not appear
          vulnerable to ReDoS.
          Details: https://sg.run/gr65

          235┆ if (!new RegExp(expectedTypes).test(valueType)) {
            ⋮┆----------------------------------------
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `property` function argument, this might allow an attacker to cause a Regular
          Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main thread. For
          this reason, it is recommended to use hardcoded regexes instead. If your regex is run on user-
          controlled input, consider performing input validation or use a regex checking/sanitization library
          such as https://www.npmjs.com/package/recheck to verify that the regex does not appear vulnerable to
          ReDoS.
          Details: https://sg.run/gr65

          235┆ if (!new RegExp(expectedTypes).test(valueType)) {

   ❯❯❱ javascript.browser.security.insecure-document-method.insecure-document-method
          User controlled data in methods like `innerHTML`, `outerHTML` or `document.write` is an anti-pattern
          that can lead to XSS vulnerabilities
          Details: https://sg.run/LwA9

          3815┆ element.innerHTML = this._config.template;
            ⋮┆----------------------------------------
          3851┆ element.innerHTML = content;

    src/main/resources/static/vendors/fontawesome/js/fontawesome.js
   ❯❯❱ javascript.browser.security.insecure-document-method.insecure-document-method
          User controlled data in methods like `innerHTML`, `outerHTML` or `document.write` is an anti-pattern
          that can lead to XSS vulnerabilities
          Details: https://sg.run/LwA9

          630┆ style.innerHTML = css;
            ⋮┆----------------------------------------
          1360┆ node.outerHTML = newOuterHTML + (config.keepOriginalSource && node.tagName.toLowerCase()
               !== 'svg' ? "<!-- ".concat(node.outerHTML, " Font Awesome fontawesome.com -->") : '');
            ⋮┆----------------------------------------
          1364┆ newNode.outerHTML = newOuterHTML;
            ⋮┆----------------------------------------
          1397┆ node.innerHTML = newInnerHTML;
            ⋮┆----------------------------------------
          2056┆ element.outerHTML = abstract.map(function (a) {
          2057┆   return toHtml(a);
          2058┆ }).join('\n');
            ⋮┆----------------------------------------
          2190┆ container.innerHTML = val.html;

    src/main/resources/static/vendors/jquery-mask/Dockerfile
   ❯❯❱ dockerfile.security.missing-user.missing-user
          By not specifying a USER, a program in the container may run as 'root'. This is a security hazard.
          If an attacker can control a process running as root, they may have control over the container.
          Ensure that the last USER in a Dockerfile is a USER other than 'root'.
          Details: https://sg.run/Gbvn

           ▶▶┆ Autofix ▶ USER non-root CMD ["/sbin/my_init"]
            4┆ CMD ["/sbin/my_init"]

    src/main/resources/static/vendors/jquery-mask/deploy.rb
    ❯❱ ruby.lang.security.dangerous-subshell.dangerous-subshell
          Detected non-static command inside `...`. If unverified user data can reach this call site, this is
          a code injection vulnerability. A malicious actor can inject a malicious script to execute arbitrary
          code.
          Details: https://sg.run/NrxL

           44┆ `git commit -am 'generating jquery mask files #{JMASK_VERSION}'`

    src/main/resources/static/vendors/jquery-mask/src/jquery.mask.js
    ❯❱ javascript.lang.security.audit.detect-non-literal-regexp.detect-non-literal-regexp
          RegExp() called with a `mask` function argument, this might allow an attacker to cause a Regular
          Expression Denial-of-Service (ReDoS) within your application as RegExP blocks the main thread. For
          this reason, it is recommended to use hardcoded regexes instead. If your regex is run on user-
          controlled input, consider performing input validation or use a regex checking/sanitization library
          such as https://www.npmjs.com/package/recheck to verify that the regex does not appear vulnerable to
          ReDoS.
          Details: https://sg.run/gr65

          165┆ r = r.replace(new RegExp('(' + oRecursive.digit + '(.*' + oRecursive.digit + ')?)'),
               '($1)?')
            ⋮┆----------------------------------------
          166┆ .replace(new RegExp(oRecursive.digit, 'g'), oRecursive.pattern);
            ⋮┆----------------------------------------
          169┆ return new RegExp(r);



┌──────────────┐
│ Scan Summary │
└──────────────┘
✅ Scan completed successfully.
 • Findings: 24 (24 blocking)
 • Rules run: 448
 • Targets scanned: 1798
 • Parsed lines: ~99.9%
 • Scan skipped:
   ◦ Files larger than  files 1.0 MB: 2
   ◦ Files matching .semgrepignore patterns: 30
 • Scan was limited to files tracked by git
 • For a detailed list of skipped files and lines, run semgrep with the --verbose flag
Ran 448 rules on 1798 files: 24 findings.
```

W sumie zostały wykryte 24 błędy.

## Zadanie 3
Do deploymentu został utworzony plik [gc_security_scan.yaml](.github/workflows/gc_security_scan.yaml). Treść pliku:
```
name: Github Action Security Scan

on:
  push:
    branches: [ "main" ]

jobs:
  security-tests:
    runs-on: ubuntu-latest

    steps:
      - name: Check out code
        uses: actions/checkout@v3

      - name: Build Docker image
        run: |
          docker build -t myapp:latest .

      - name: Run Trivy scan
        uses: aquasecurity/trivy-action@0.10.0
        with:
          image-ref: 'myapp:latest'
          format: 'table'

      - name: Install Semgrep
        run: |
          pip install semgrep

      - name: Run Semgrep
        run: |
          semgrep --config p/security-audit src
```

Wyniki Github Actions dla joba: [Wyniki joba github actions](https://github.com/Yibux/task4/actions/runs/20247273118)
![Zadanie 3 - wyniki Github Actions](https://github.com/Yibux/task4/blob/main/zad3_1.png?raw=true)
![Zadanie 3 - wyniki Trivy](https://github.com/Yibux/task4/blob/main/zad3_2.png?raw=true)
![Zadanie 3 - wyniki Trivy](https://github.com/Yibux/task4/blob/main/zad3_3.png?raw=true)
![Zadanie 3 - wyniki Semgrep](https://github.com/Yibux/task4/blob/main/zad3_4.png?raw=true)

## Zadanie 4
Wyniki analizy ZAP:
![Zadanie 4 - analiza ZAP](https://github.com/Yibux/task4/blob/main/zad4_1.png?raw=true)
![Zadanie 4 - analiza ZAP](https://github.com/Yibux/task4/blob/main/zad4_2.png?raw=true)