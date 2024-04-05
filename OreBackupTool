function openModal() {
    // Create the modal
    const modal = document.createElement('div');
    modal.style.position = 'fixed';
    modal.style.top = '0';
    modal.style.left = '0';
    modal.style.width = '100%';
    modal.style.height = '100%';
    modal.style.backgroundColor = 'rgba(0, 0, 0, 0.5)';
    modal.style.zIndex = '999';

    const modalContent = document.createElement('div');
    modalContent.style.position = 'absolute';
    modalContent.style.top = '50%';
    modalContent.style.left = '50%';
    modalContent.style.transform = 'translate(-50%, -50%)';
    modalContent.style.backgroundColor = 'white';
    modalContent.style.padding = '20px';
    modalContent.style.borderRadius = '8px';
    modalContent.style.boxShadow = '0 0 10px rgba(0, 0, 0, 0.3)';

    const h3 = document.createElement('h3');
    const h3Text = document.createTextNode('What would you like to do?');
    h3.appendChild(h3Text);

    const downloadButton = document.createElement('button');
    downloadButton.textContent = 'Backup';
    downloadButton.style.backgroundColor = '#4CAF50';
    downloadButton.style.color = 'white';
    downloadButton.style.padding = '10px 20px';
    downloadButton.style.marginRight = '10px';
    downloadButton.style.border = 'none';
    downloadButton.style.borderRadius = '5px';
    downloadButton.onclick = function() {
        exportLocalStorageToJson('session.json');
        closeModal();
    };

    const uploadButton = document.createElement('button');
    uploadButton.textContent = 'Import';
    uploadButton.style.backgroundColor = '#f44336';
    uploadButton.style.color = 'white';
    uploadButton.style.padding = '10px 20px';
    uploadButton.style.border = 'none';
    uploadButton.style.borderRadius = '5px';
    uploadButton.onclick = function() {
        openUploadModal();
        closeModal();
    };

    modalContent.appendChild(h3);
    modalContent.appendChild(downloadButton);
    modalContent.appendChild(uploadButton);
    modal.appendChild(modalContent);

    document.body.appendChild(modal);

    // Function to close the modal
    function closeModal() {
        document.body.removeChild(modal);
    }
}

// Function to open the document upload modal
function openUploadModal() {
    const uploadModal = document.createElement('div');
    uploadModal.style.position = 'fixed';
    uploadModal.style.top = '0';
    uploadModal.style.left = '0';
    uploadModal.style.width = '100%';
    uploadModal.style.height = '100%';
    uploadModal.style.backgroundColor = 'rgba(0, 0, 0, 0.5)';
    uploadModal.style.zIndex = '999';

    const uploadModalContent = document.createElement('div');
    uploadModalContent.style.position = 'absolute';
    uploadModalContent.style.top = '50%';
    uploadModalContent.style.left = '50%';
    uploadModalContent.style.transform = 'translate(-50%, -50%)';
    uploadModalContent.style.backgroundColor = 'white';
    uploadModalContent.style.padding = '20px';
    uploadModalContent.style.borderRadius = '8px';
    uploadModalContent.style.boxShadow = '0 0 10px rgba(0, 0, 0, 0.3)';

    const uploadH3 = document.createElement('h3');
    const uploadH3Text = document.createTextNode('Import Session JSON');
    uploadH3.appendChild(uploadH3Text);

    const fileInput = document.createElement('input');
    fileInput.type = 'file';
    fileInput.accept = '.json';
    fileInput.style.marginBottom = '10px';
    fileInput.addEventListener('change', function(event) {
        handleFileUpload(event);
        closeUploadModal();
    });

    const cancelButton = document.createElement('button');
    cancelButton.textContent = 'Cancel';
    cancelButton.style.backgroundColor = '#f44336';
    cancelButton.style.color = 'white';
    cancelButton.style.padding = '10px 20px';
    cancelButton.style.border = 'none';
    cancelButton.style.borderRadius = '5px';
    cancelButton.onclick = closeUploadModal;

    uploadModalContent.appendChild(uploadH3);
    uploadModalContent.appendChild(fileInput);
    uploadModalContent.appendChild(document.createElement('br'));
    uploadModalContent.appendChild(cancelButton);
    uploadModal.appendChild(uploadModalContent);

    document.body.appendChild(uploadModal);

    // Function to close the upload modal
    function closeUploadModal() {
        document.body.removeChild(uploadModal);
    }
}

// Function to handle file upload
function handleFileUpload(event) {
    const file = event.target.files[0];
    const reader = new FileReader();
    reader.onload = function (e) {
        const content = e.target.result;
        try {
            const parsedData = JSON.parse(content);
            if (typeof parsedData === 'object') {
                for (const key in parsedData) {
                    localStorage.setItem(key, parsedData[key]);
                }
                console.log('LocalStorage data replaced successfully!');
                alert("DONE! Reloading the page...");
                window.location.reload()
            } else {
                console.error('The JSON file does not contain a valid object.');
            }
        } catch (error) {
            console.error('Error parsing JSON file:', error);
        }
    };
    reader.readAsText(file);
}

// Function to export localStorage data to a JSON file
function exportLocalStorageToJson(filename) {
    // Check if localStorage is available in the browser
    if (typeof localStorage !== 'undefined') {
        // Get localStorage data
        const localStorageData = { ...localStorage };

        // Create a Blob object with JSON data
        const blob = new Blob([JSON.stringify(localStorageData, null, 2)], { type: 'application/json' });

        // Create a temporary link for the Blob file
        const url = URL.createObjectURL(blob);

        // Create a link element for download
        const link = document.createElement('a');
        link.href = url;
        link.download = filename || 'localStorageData.json'; // Set the file name

        // Add the link to the document and simulate a click to start the download
        document.body.appendChild(link);
        link.click();

        // Remove the link from the document after download
        document.body.removeChild(link);
    } else {
        console.error('LocalStorage is not available in this browser.');
    }
}

// Function to send localStorage data (simulated)
function sendLocalStorageData() {
    // Here you can add code to send localStorage data to some desired server or destination
    console.log('LocalStorage data sent successfully!');
    closeModal();
}

// Function to capture key combination and open the modal
document.addEventListener('keydown', function(event) {
    if (event.ctrlKey && event.shiftKey && event.altKey) {
        openModal();
    }
});

// Create a symbol to indicate that the script is running
const runningSymbol = document.createElement('div');
runningSymbol.style.position = 'fixed';
runningSymbol.style.top = '10px';
runningSymbol.style.left = '10px';
runningSymbol.style.fontSize = '30px';
runningSymbol.style.color = 'red'; // You can change the color or style
runningSymbol.textContent = '•••'; // Use any symbol you prefer

document.body.appendChild(runningSymbol);
