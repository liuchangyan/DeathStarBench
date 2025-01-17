# Hotel Reservation Knative workloads

The application implements a hotel reservation 
service, build with Go and gRPC, and starting from the open-source project https://github.com/harlow/go-micro-services. The initial project is extended in several ways, including adding back-end in-memory and persistent databases, adding a recommender system for 
obtaining hotel recommendations, and adding the functionality to place a hotel
reservation. 


**Hotel Reservation** includes the relationships of end-to-end services are as follows:
 
<img src="hotelReservation_architecture.png"/>

In **Knative workloads**, the services marked **Green** are refactored from k8s services to Knative services:

<img src="hotelReservation_knative.
png"/>

The ``Frontend Service`` and the      ``Backend storage services`` are not transfered to knative, which represents the middle layer mostly deal with the high volumes of HTTP traffic in FaaS workloads.


## Pre-requirements
- Kubernates
- Knative-serving
- Istio

## Running the hotel reservation application
### Before you start

- Make sure your kubernetes cluster running steadily
- Install ``Knative-serving`` and ``Istio``
    - Install ``knative-serving`` following Doc:     
    [Install Serving](https://knative.dev/docs/install/yaml-install/serving/install-serving-with-yaml/#install-the-knative-serving-component)
    - Install`` a networking layer Istio`` following Doc:     
    [Install a networking layer Istio for knative](https://knative.dev/docs/install/yaml-install/serving/install-serving-with-yaml/#install-a-networking-layer)
    - Configuring DNS following Doc:                
    [Configuring DNS for Istio](https://knative.dev/docs/install/installing-istio/#verifying-your-istio-install)

## Deploy Knative services in kubernetes:
### Build images:
```bash
cd <path-of-repo>/hotelReservation/knative/
scripts
./update-config.sh
cd ../..
docker build . -t $yourdockername
```
### Deploy services in kubernetes
```bash
cd <path-of-repo>/hotelReservation/knative/scripts
./deploy-knative-svc.sh
```
