# Project-Atlas
Initial Map Functionality

//Below is the code written so far in Swift and I am using Xcode 8.2.1. I am trying to build a map/navigation application. My //initial desired functionality is to use Mapbox in the Main.Storyboard (rather than MapKit) and then CoreLocation to handle //the functionality of the GPS chip (i.e pulling latitude, longitude, accuracy, speed, etc.).

//Here is where I'm having difficulty: I was able to successfully import Mapbox and CoreLocation, however once I tried to center the map on the user's latitude and longitude, this is where the errors began. I am simply trying to have the map zoom in on the user latitudes and longitude and ultimately have tracking functionality available as well. At some point I want able to build the simulated app and it was printing the latitude and longitude perfectly fine in the Out area. Once I added in code to center the mapView, that is where I ran into issues. To further complicate the process, the tutorial I have been viewing was written for MapKit so I have had to translate MapKit code to Mapbox code as necessary.

//Here is the code. Any help letting me know what I am doing wrong is greatly appreciated:

//
//  ViewController.swift
//  Atlas
//
//  Created by Vscout on 1/29/17.
//  Copyright © 2017 Vscout. All rights reserved.
//

import UIKit
import Mapbox
import CoreLocation

class ViewController: UIViewController, CLLocationManagerDelegate, MGLMapViewDelegate {
    
    @IBOutlet var map: MGLMapView!
    
    var locationManager = CLLocationManager()

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let mapView = MGLMapView(frame: view.bounds)
        
        view.addSubview(mapView)

        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyBest
        locationManager.requestWhenInUseAuthorization()
        locationManager.startUpdatingLocation()
        
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }

    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        
        let userLocation: CLLocation = locations[0]
        
        let latitude = userLocation.coordinate.latitude
        
        let longitude = userLocation.coordinate.longitude
        
        let latDelta: CLLocationDegrees = 0.05
        
        let lonDelta: CLLocationDegrees = 0.05
        
        let span = MGLCoordinateSpan(latitudeDelta: latDelta, longitudeDelta: lonDelta)
        
        let location = CLLocationCoordinate2D(latitude: latitude, longitude: longitude)
        
        let center = CLLocationCoordinate2D(latitude: latitude, longitude: longitude)
        
//Error is occurring on line 65 and 67. Error "Use of unresolved identifier 'mapView' on both lines
        mapView.setCenter(center, zoomLevel: 15, animated: true)
        
        mapView.userTrackingMode = .follow

    }

}
