//
//  ViewController.swift
//  Chip the Sandwich Making Chatbot
//
//  Created by Nathan Rowbottom on 2/6/2019.
//  Copyright © 2019 Crow Stile Solutions. All rights reserved.
//

import UIKit
import ApiAI
import AVFoundation

class ViewController: UIViewController, AVSpeechSynthesizerDelegate {

    @IBOutlet weak var messageField: UITextField!
    @IBOutlet weak var chipResponse: UILabel!
    @IBAction func sendMessage(_ sender: Any) {
        let request = ApiAI.shared()?.textRequest()
        
        if let text = self.messageField.text, text != "" {
            request?.query = text
        } else{
            return
        }
        
        request?.setMappedCompletionBlockSuccess({ (request, response) in
            let response = response as! AIResponse
            if let textResponse = response.result.fulfillment.value(forKeyPath: "speech") as! String? {
                self.speechAndText(text: textResponse)
                print(textResponse)
            }
        }, failure: { (request, error) in
            print(error!)
        })
        
        ApiAI.shared()?.enqueue(request)
        messageField.text = ""
    }
    
    let speech = AVSpeechSynthesizer()
    
    func speechAndText( text:String){
        //let utterance = AVSpeechUtterance(string: text)
        let utterance = AVSpeechUtterance(string: text)
        utterance.voice = AVSpeechSynthesisVoice(language: "en_US")
        //let voice = AVSpeechSynthesizer()
        
        speech.delegate = self
       //speech.speak(utterance)
        
        self.chipResponse.text = text
        self.speech.speak(utterance)
        //print(utterance)
        
        UIView.animate(withDuration: 1.0, delay: 0.0, options: .curveEaseInOut, animations: {self.chipResponse.text = text}, completion: nil)
    
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }

    func speechSynthesizer(_ synthesizer: AVSpeechSynthesizer, didFinish utterance: AVSpeechUtterance) {
       //print("delegate mthod did finish worked\(utterance)")
    }
    
    func speechSynthesizer(_ synthesizer: AVSpeechSynthesizer, willSpeakRangeOfSpeechString characterRange: NSRange, utterance: AVSpeechUtterance) {
     
    }
}

