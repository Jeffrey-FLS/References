# Webstorm Tips



### Tip 1 - When starting a new project and wanting to set the relative path in webstorm, create the `.env` file on the root directory of the project (react practices), set the Node location inside the file, with the optional API location 

```.env
NODE_PATH=src/
REACT_APP_BASE_URL=http://localhost:3000/api/v1
```

### Afterwards, right click on the `src` directory inside Webstorm and under "Mark Directory as" select "Resource Root". Now everytime you invoke an import of a file, just start with the directory name or file within the src directory. IE:

```javascript
import imgPlaceholder from 'assets/images/img-placeholder.png';
```



### Tip 2 - Webstorm cannot resolve symbol

#### In order to avoid the imported components and libraries to be tagged with a "cannot resolve symbol" you must download the type library for that. In example, React Router Dom Switch will be tagged as an error. To avoid this, go to `File > Settings > Languages & Frameworks > Javascript > Libraries `  and Download `react-dom-router`. The same is applied whenever react components are being tagged, just download the `react` types file.



### Tip 3 - 

