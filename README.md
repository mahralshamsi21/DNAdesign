# DNAdesign
import random
import string
import requests

def generate_dna_sequence(length):
    bases = ['A', 'T', 'C', 'G']
    sequence = ''.join(random.choice(bases) for _ in range(length))
    return sequence

def save_to_github(filename, content):
    # Your GitHub repository URL
    repo_url = "https://github.com/mahralshamsi21/DNAdesign"
    
    # Personal access token for authentication
    access_token = "your_access_token"

    # File path within the repository
    file_path = "path/to/folder/" + filename
    
    # API endpoint for creating a file
    api_url = f"https://api.github.com/repos/{repo_url}/contents/{file_path}"
    
    # Create the request headers
    headers = {
        "Authorization": f"Bearer {access_token}",
        "Accept": "application/vnd.github.v3+json"
    }
    
    # Create the request payload
    payload = {
        "message": "Adding DNA sequence",
        "content": content
    }
    
    # Send a PUT request to create or update the file
    response = requests.put(api_url, headers=headers, json=payload)
    
    if response.status_code == 201:
        print("File created successfully.")
    elif response.status_code == 200:
        print("File updated successfully.")
    else:
        print("An error occurred while saving the file.")

# Generate a DNA sequence of length 100
sequence_length = 100
dna_sequence = generate_dna_sequence(sequence_length)

# Save the DNA sequence to a file on GitHub
filename = "dna_sequence.txt"
save_to_github(filename, dna_sequence) 
