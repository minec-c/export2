name: Export Godot HTML5

on:
  workflow_dispatch:
  
permissions:
  contents: write
  
jobs:
  export-web:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4



      - name: Download Godot
        run: |
          wget https://github.com/godotengine/godot/releases/download/3.4-stable/Godot_v3.4-stable_linux_headless.64.zip
      
          unzip Godot_v3.4-stable_linux_headless.64.zip
      
          chmod +x Godot_v3.4-stable_linux_headless.64



      - name: Download Export Templates
        run: |
          wget https://github.com/godotengine/godot/releases/download/3.4-stable/Godot_v3.4-stable_export_templates.tpz

          mkdir templates
          
          unzip Godot_v3.4-stable_export_templates.tpz -d templates
          
          mkdir -p ~/.local/share/godot/templates/3.4.stable
          
          cp templates/templates/webassembly_* \
          ~/.local/share/godot/templates/3.4.stable/

      - name: Export project
        run: |
          mkdir -p g340/build
      
          cd g340
      
          ../Godot_v3.4-stable_linux_headless.64 \
          --headless \
          --export "HTML5" build/index.html

      - name: Commit generated files
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "github-actions@github.com"
      
          git add g340/build/
          git commit -m "Export HTML5 build" || echo "No changes"
          git push
