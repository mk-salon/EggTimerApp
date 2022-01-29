# EggTimerApp

```swift
import UIKit
import AVFoundation

class ViewController: UIViewController {
    
    @IBOutlet weak var titleLabel: UILabel!
    @IBOutlet weak var progressBar: UIProgressView!
    let eggTimes: [String: Float] = ["Soft": 300, "Medium": 420, "Hard": 720]
    var timer = Timer()
    var totaltime: Float = 0
    var secondsPast: Float = 0
    var player: AVAudioPlayer!
    
    @IBAction func hardnessSelected(_ sender: UIButton) {
        timer.invalidate()
        let hardness = sender.currentTitle!
        totaltime = eggTimes[hardness]!
        titleLabel.text = hardness
        progressBar.progress = 0.0
        secondsPast = 0
    
        timer = Timer.scheduledTimer(timeInterval: 1.0, target: self, selector: #selector(updateTimer), userInfo: nil, repeats: true)
    }
    
    @objc func updateTimer() {
        if secondsPast < totaltime {
            secondsPast += 1
            progressBar.progress = secondsPast / totaltime
        } else {
            timer.invalidate()
            titleLabel.text = "Done!"
            playSound(soundName: "alarm_sound")  
        }
    }
    
    func playSound(soundName: String) {
        let url = Bundle.main.url(forResource: soundName, withExtension: "mp3")
        player = try! AVAudioPlayer(contentsOf: url!)
        player.play()
        
    }
}
```
