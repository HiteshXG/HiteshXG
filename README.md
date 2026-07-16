name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *"  # Runs daily at midnight
  workflow_dispatch:  # Allows manual trigger

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3
        
      - name: Generate Snake
        uses: Platane/snk@v3
        with:
          github_user_name: HiteshXG  # Change to your username
          outputs: |
            output/github-contribution-grid-snake.svg
            output/github-contribution-grid-snake-dark.svg?palette=github-dark
          
      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: output
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
