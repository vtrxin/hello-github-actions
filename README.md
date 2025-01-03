<name: Windows Cloud PC - Anydesk (Optimized)

on:
  workflow_dispatch:

jobs:
  build:
    name: Start Building...
    runs-on: windows-latest
    timeout-minutes: 10080  # MÃ¡ximo de 7 dias para evitar tempo de execuÃ§Ã£o excessivo

    steps:
      - name: Downloading & Installing Essentials
        run: |
          # Baixa o arquivo .bat para instalar componentes essenciais
          Invoke-WebRequest -Uri "https://www.dropbox.com/scl/fi/7eiczvgil84czu55dxep3/Downloads.bat?rlkey=wzdc1wxjsph2b7r0atplmdz3p&dl=1" -OutFile "Downloads.bat"
          # Executa o script .bat para instalar os componentes
          cmd /c Downloads.bat

      - name: Log In To AnyDesk
        run: |
          # Verifica se o arquivo start.bat existe antes de executar
          if (Test-Path "start.bat") {
            cmd /c start.bat
          } else {
            Write-Host "Arquivo start.bat nÃ£o encontrado. Verifique a configuraÃ§Ã£o."
          }

      - name: Monitor and Restart AnyDesk if Needed
        run: |
          # Monitora a conexÃ£o do AnyDesk e reinicia se necessÃ¡rio
          while ($true) {
            $process = Get-Process -Name "AnyDesk" -ErrorAction SilentlyContinue
            if (-not $process) {
              Write-Host "AnyDesk nÃ£o estÃ¡ rodando, reiniciando..."
              cmd /c start.bat
            }
            Start-Sleep -Seconds 300  # Verifica a cada 5 minutos
          }

      - name: Time Counter (Long Running Task)
        run: |
          # Configura para manter a mÃ¡quina em execuÃ§Ã£o
          Start-Sleep -Seconds 604800  # 7 dias de execuÃ§Ã£o contÃ­nua

      - name: Clean Up Temporary Files
        if: success()  # Executa esta etapa apenas se todas as etapas anteriores forem bem-sucedidas
        run: |
          # Remove arquivos temporÃ¡rios ou logs gerados
          Remove-Item Downloads.bat -Force
          Write-Host "Limpeza completa."

# Hello GitHub Actions

_Create and run a GitHub Actions workflow._

</header>

## Welcome

Automation is key for streamlining your work processes, and [GitHub Actions](https://docs.github.com/actions) is the best way to supercharge your workflow.

- **Who is this for**: Developers, DevOps engineers, students, managers, teams, GitHub users.
- **What you'll learn**: How to create workflow files, trigger workflows, and find workflow logs.
- **What you'll build**: An Actions workflow that will check emoji shortcode references in Markdown files.
- **Prerequisites**: In this course you will work with issues and pull requests, as well as edit files. We recommend you take the [Introduction to GitHub](https://github.com/skills/introduction-to-github) course first.
- **How long**: This course can be finished in less than two hours.

In this course, you will:

1. Create a workflow
2. Add a job
3. Add a run step
4. Merge your pull request
5. See effect of the workflow

### How to start this course

[![start-course](https://user-images.githubusercontent.com/1221423/235727646-4a590299-ffe5-480d-8cd5-8194ea184546.svg)](https://github.com/new?template_owner=skills&template_name=hello-github-actions&owner=%40me&name=skills-hello-github-actions&description=My+clone+repository&visibility=public)

1. Right-click **Start course** and open the link in a new tab.
2. In the new tab, most of the prompts will automatically fill in for you.
   - For owner, choose your personal account or an organization to host the repository.
   - We recommend creating a public repository, as private repositories will [use Actions minutes](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions).
   - Scroll down and click the **Create repository** button at the bottom of the form.
3. After your new repository is created, wait about 20 seconds, then refresh the page. Follow the step-by-step instructions in the new repository's README.

<footer>

---

Get help: [Post in our discussion board](https://github.com/orgs/skills/discussions/categories/hello-github-actions) &bull; [Review the GitHub status page](https://www.githubstatus.com/)

&copy; 2023 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

</footer>
