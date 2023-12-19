# Images_Userway

const imgAltScanner = () => {
    const images = document.getElementsByTagName("img");

    const clickHandler = (el) => {
      const field = document.createElement("INPUT");
      field.setAttribute("type", "text");
      const selectedImage = el.target;
      field.setAttribute("value", selectedImage.id);
      field.setAttribute("id", `x+"${selectedImage.id}`);
      field.style.cssText = `
      position: absolute;
        border: 5px solid blue;
        left: 50%;
        top: 50%;
        z-index: 10
      `;
      document.body.appendChild(field);
      const changeAltName = (inputText) => {
        selectedImage.setAttribute("alt", inputText.target.value);
      };
      field.addEventListener("input", changeAltName);
    };

    Array.from(images).forEach(async (img) => {
      const altName = await fetch("https://random-word-api.herokuapp.com/word?lang=it")
        .then((response) => response.json())
        .then((response) => response[0]);
      img.setAttribute("style", "border: 10px solid blue; border-radius: 5px");
      img.setAttribute("id", altName);
      img.setAttribute("alt", altName);
      img.addEventListener("click", clickHandler);
    });
    return images;
  };
