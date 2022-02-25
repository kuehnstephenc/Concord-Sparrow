# Setup for running importer scripts & GUI (MacOS)
```
1 - "python3 -m venv env"
2 - "source env/bin/activate"
3 - "python3 -m pip install --upgrade pip"
4 - "pip install -r requirements.txt" 
5 - "cd importers"
6 - "python /importers/dataCleaner.py"
```

## Steps to get sparrow working
```
in your terminal
1 - bash -c "$(curl -fsSL https://raw.githubusercontent.com/EarthCubeGeochron/Sparrow/HEAD/get-sparrow.sh)"
2 - make sure Docker has been updated and is currently running with sufficient memory allocation(>=4GB)
3 - make sure you're in the sparrow folder
4 - you should be able to run "sparrow" with no errors
5 - SPARROW_SECRET_KEY=TemporaryKey sparrow up
6 - go to localhost:5002
```

## Priority
- [] Add the new tables and fields to the database; Document these carefully; Write a script which would re-create these on a new Sparrow installation
- [] Start putting the sample catalog and related things in Sparrow (try to make this as easy as copy and paste)
- [] Switch from using Google sheets to using Sparrow directly for #2 - This will require setting up an user interface to the DB and setting up an importer for sample information exported from StraboSpot
- [] Start developing the Sparrow website
- [] Start importing other kinds of data, linking images/photos, etc.

- [ ] allow batch processing 
- [x] allow users to make a list of files to run batch process on! - GUI
- [ ] Schema for database  - https://sparrow-data.org/docs/motivation-and-design
- [ ] Add more testing for data cleaner class
- [ ] Json export * https://github.com/EarthCubeGeochron/Sparrow/blob/main/backend/sparrow_tests/fixtures/large-test.json
  - [ ] https://earthchem.org/communities/tephra/
  - [ ] https://zenodo.org/record/4075613#.YUzSAi1h3zJ
- [ ] Importer file https://github.com/EarthCubeGeochron/Sparrow-CU-TRaIL/blob/a9089678891d24af1c2440f575d64ac26285377a/plugins/import_reduction_sheet/importer.py#L280

- [] samples schema json - StraboSpot_output file in excel files dir
  - sample label as sample name

importer schemas
- [ ] project
- [ ] sample
- [ ] session 
- [ ] instrument
- [ ] analysis
- [ ] datum
- [ ] datafile
- [ ] sample


# Deploying Sparrow on a Digital Ocean droplet
- Sign in with Github
- Create a team - https://docs.digitalocean.com/products/accounts/teams/quickstart/
- Go to billing and add PROMO CODE : ACTIVATE60
- Droplet configuration/type : Basic - Shared CPU - 4 vCPUs - 8 GB - 160 GB - 5 TB - $40/month
- Open the console online and enter the following commands

```
sudo apt-get update 

sudo apt-get install ca-certificates curl gnupg lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

bash -c "$(curl -fsSL https://sparrow-data.org/get-sparrow.sh)"

sudo docker run hello-world

sparrow

SPARROW_SECRET_KEY=TemporaryKey sparrow up
```

- <ipv4 address from droplet dashboard>:5002/  - frontend port number (5002)
  - i.e 157.245.92.59:5002/