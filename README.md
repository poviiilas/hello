# hello
fetch('https://1drv.ms/x/s!Ag5QM8M-Ff7ouLo3zQN5nW2yaQUjkw?e=aHUTvB')
  .then(response => response.json())
  .then(data => {
    const jsonString = JSON.stringify(data, null, 2);

    fetch('https://api.github.com/gists', {
      method: 'POST',
      body: JSON.stringify({
        files: {
          'data.json': {
            content: jsonString
          }
        },
        public: true,
        description: 'Shared JSON Data'
      })
    })
      .then(response => response.json())
      .then(gistData => {
        const gistId = gistData.id;
        const gistUrl = `https://gist.github.com/${gistId}`;
        console.log('Shared URL:', gistUrl);
      })
      .catch(error => console.error('Error creating Gist:', error));
  })
  .catch(error => console.error('Error fetching JSON data:', error));
