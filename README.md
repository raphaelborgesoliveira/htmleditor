<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" type="text/css" href="style.css">
  </head>
  <body>
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.15.1/css/all.css" integrity="sha384-vp86vTRFVJgpjF9jiIGPEEqYqlDwgyBgEF109VFjmqGmIY/Y4HV4d3Gp2irVfcrp" crossorigin="anonymous">


    <div class="container">
      <div class="left-pane">
        <div contenteditable="true" id="text-pane"></div>
      </div>
      <div class="right-pane">
        <pre id="code-pane" contenteditable="true"></pre>
      </div>
    </div>
    <div class="toolbar">
      <button onclick="execCommandWithArg('bold', null)"><b><i class="fas fa-bold"></i>
      <button onclick="execCommandWithArg('italic', null)">
        <i>
          <i class="fa fa-italic"></i>
      <button onclick="execCommandWithArg('underline', null)">
        <u>
          <i class="fa fa-underline"></i>
      <button onclick="execCommandWithArg('insertOrderedList', null)">
        <i class="fa fa-list-ol"></i>
      <button onclick="execCommandWithArg('insertUnorderedList', null)">
        <i class="fa fa-list-ul"></i>
      <button onclick="execCommandWithArg('justifyLeft', null)">
        <i class="fa fa-align-left"></i>
      <button onclick="execCommandWithArg('justifyCenter', null)">
        <i class="fa fa-align-center"></i>
      <button onclick="execCommandWithArg('justifyRight', null)">
        <i class="fa fa-align-right"></i>
      <button onclick="execCommandWithArg('justifyFull', null)">
        <i class="fa fa-align-justify"></i>
      <button onclick="execCommandWithArg('indent', null)">
        <i class="fa fa-indent"></i>
      <button onclick="execCommandWithArg('outdent', null)">
        <i class="fa fa-outdent"></i>
      <button onclick="execCommandWithArg('createLink', prompt('Insira o URL:','http://'))">
        <i class="fa fa-link"></i>
      <button onclick="execCommandWithArg('unlink', null)">
        <i class="fa fa-unlink"></i>
      <button onclick="execCommandWithArg('insertImage', prompt('Insira a URL da imagem:','http://'))">
        <i class="fa fa-image"></i>
      <button onclick="breakLines()">Quebrar linhas</button>
    
    <script>
    
        function execCommandWithArg(command, arg) {
          document.execCommand(command, false, arg);
        }
        
        const textPane = document.querySelector("#text-pane");
        const codePane = document.querySelector("#code-pane");
        textPane.addEventListener("input", updateCodePane);
        codePane.addEventListener("input", updateTextPane);
        
        function updateCodePane() {
          codePane.textContent = textPane.innerHTML;
        }
        
      function updateTextPane() {
        textPane.innerHTML = codePane.textContent.replace(/&nbsp;/g, " ");
      }

        
        document.querySelector("#indent-code-button").addEventListener("click", indentCode);

      
        function breakLines() {
          codePane.textContent = codePane.textContent.replace(/</g, "\n<").replace(/>/g, ">\n");
        }

        function indentCode() {
            const lines = codePane.innerHTML.split("\n");
            let indentation = "";
            let indentedCode = "";
            for (let i = 0; i < lines.length; i++) {
              const line = lines[i];
              if (line.startsWith("</")) {
                indentation = indentation.substring(2);
              }
              indentedCode += indentation + line + "\n";
              if (line.startsWith("<") && !line.startsWith("</")) {
                indentation += "  ";
              }
            }
            codePane.textContent = indentedCode;
          }
          
        
      </script>
