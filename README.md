### Para Iniciar esta prueba de Storybook con React necesitaremos de lo siguiente:

- Instalar yarn 
````
npm install -g yarn
````
- Instalar StoryBook ( plantilla de docs storybook )
````
npx degit chromaui/intro-storybook-react-template taskbox
````
- Descargar las dependencias de yarn con:
````
yarn
````
- Iniciar StoryBook:
````
yarn storybook
````
- En la carpeta de src crearemos otra dentro de la misma, llamada "components".
- En la carpeta de components creamos dos archivos: Task.jsx y Task.stories.jsx.
### Vamos a ir a la carpeta de storybook
- Y en el archivo de main.js pondras lo siguiente:

 ````
/** @type { import('@storybook/react-vite').StorybookConfig } */
const config = {
  stories: ['../src/components/**/*.stories.@(js|jsx)'],
   staticDirs: ['../public'],
   addons: [
     '@storybook/addon-links',
     '@storybook/addon-essentials',
     '@storybook/addon-interactions',
   ],
   framework: {
     name: '@storybook/react-vite',
     options: {},
   },
 };
 export default config;
````
- Luego en el preview.js pondras esto:

````
import '../src/index.css';

//👇 Configures Storybook to log the actions( onArchiveTask and onPinTask ) in the UI.
/** @type { import('@storybook/react').Preview } */
const preview = {
  parameters: {
    controls: {
      matchers: {
        color: /(background|color)$/i,
        date: /Date$/,
      },
    },
  },
};

export default preview;

````

####  En la carpeta de component especificamente en el archivo de Task.jsx pondras lo siguiente:

````
export default function Task({ task: { id, title, state }, onArchiveTask, onPinTask }) {
    return (
      <div className={`list-item ${state}`}>
        <label
          htmlFor={`archiveTask-${id}`}
          aria-label={`archiveTask-${id}`}
          className="checkbox"
        >
          <input
            type="checkbox"
            disabled={true}
            name="checked"
            id={`archiveTask-${id}`}
            checked={state === "TASK_ARCHIVED"}
          />
          <span
            className="checkbox-custom"
            onClick={() => onArchiveTask(id)}
          />
        </label>
  
        <label htmlFor={`title-${id}`} aria-label={title} className="title">
          <input
            type="text"
            value={title}
            readOnly={true}
            name="title"
            id={`title-${id}`}
            placeholder="Input title"
          />
        </label>
        {state !== "TASK_ARCHIVED" && (
          <button
            className="pin-button"
            onClick={() => onPinTask(id)}
            id={`pinTask-${id}`}
            aria-label={`pinTask-${id}`}
            key={`pinTask-${id}`}
          >
            <span className={`icon-star`} />
          </button>
        )}
      </div>
    );
  }
  ````
  ####  Siguiendo el mismo paso en el archivo de Task.stories.jsx pondras lo siguiente:

  ````
  export default function Task({ task: { id, title, state }, onArchiveTask, onPinTask }) {
    return (
      <div className={`list-item ${state}`}>
        <label
          htmlFor={`archiveTask-${id}`}
          aria-label={`archiveTask-${id}`}
          className="checkbox"
        >
          <input
            type="checkbox"
            disabled={true}
            name="checked"
            id={`archiveTask-${id}`}
            checked={state === "TASK_ARCHIVED"}
          />
          <span
            className="checkbox-custom"
            onClick={() => onArchiveTask(id)}
          />
        </label>
  
        <label htmlFor={`title-${id}`} aria-label={title} className="title">
          <input
            type="text"
            value={title}
            readOnly={true}
            name="title"
            id={`title-${id}`}
            placeholder="Input title"
          />
        </label>
        {state !== "TASK_ARCHIVED" && (
          <button
            className="pin-button"
            onClick={() => onPinTask(id)}
            id={`pinTask-${id}`}
            aria-label={`pinTask-${id}`}
            key={`pinTask-${id}`}
          >
            <span className={`icon-star`} />
          </button>
        )}
      </div>
    );
  }
  ````
