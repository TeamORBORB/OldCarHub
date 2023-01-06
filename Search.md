<!DOCTYPE html>

<html>
<div id="searchbox"></div>
<html>

<script>


import { searchBox } from 'instantsearch.js/es/widgets';

const { searchBox } = instantsearch.widgets;
// or directly use instantsearch.widgets.searchBox()

  searchBox({
  container: string|HTMLElement,
  // Optional parameters
  placeholder: string,
  autofocus: boolean,
  searchAsYouType: boolean,
  showReset: boolean,
  showSubmit: boolean,
  showLoadingIndicator: boolean,
  queryHook: function,
  templates: object,
  cssClasses: object,
});

// Create a render function
const renderSearchBox = (renderOptions, isFirstRender) => {
  const { query, refine, clear, isSearchStalled, widgetParams } = renderOptions;

  if (isFirstRender) {
    const input = document.createElement('input');

    const loadingIndicator = document.createElement('span');
    loadingIndicator.textContent = 'Loading...';

    const button = document.createElement('button');
    button.textContent = 'X';

    input.addEventListener('input', event => {
      refine(event.target.value);
    });

    button.addEventListener('click', () => {
      clear();
    });

    widgetParams.container.appendChild(input);
    widgetParams.container.appendChild(loadingIndicator);
    widgetParams.container.appendChild(button);
  }

  widgetParams.container.querySelector('input').value = query;
  widgetParams.container.querySelector('span').hidden = !isSearchStalled;
};

// create custom widget
const customSearchBox = connectSearchBox(
  renderSearchBox
);

// instantiate custom widget
search.addWidgets([
  customSearchBox({
    container: document.querySelector('#searchbox'),
  })
]);
<script>