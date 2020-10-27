# THE NEXT CAR

The Next Car adalah sebuah contoh project MVC yang dibuat dengan tujuan pada keamanan saat mengendarai mobil.

## Scope of Functionalities
- Apa kegunaan DoorController.cs?
- Apa kegunaan Model Door.cs?
- Apa kegunaan Interface OnDoorChanged ?

### DoorController.cs
DoorController berfungsi untuk mengetahui apakah udah terLock atau belum pintu dari mobil itu.

``` javascript
namespace TheNextCar.Controller
{
    class DoorController
    {
        private Door door;
        private OnDoorChanged callbackOnDoorChanged;

        public DoorController(OnDoorChanged callbackOnDoorChanged)
        {
            this.callbackOnDoorChanged = callbackOnDoorChanged;
            this.door = new Door();
        }
```
### Door.cs
Door.cs berfungsi untuk mengetahui fungsi door Closed atau Locked.
``` C#
namespace TheNextCar.Model
{
    class Door
    {
        private bool locked;
        private bool closed;

        public void close()
        {
            this.closed = true;
        }

        public void open()
        {
            this.closed = false;
        }

        public void activatelock()
        {
            this.locked = true;
        }

        public void unlock()
        {
            this.locked = false;
        }

        public bool isLocked()
        {
            return this.locked;
        }

        public bool isClosed()
        {
            return this.closed;
        }
    }
}
```
### OnDoorChanged
OnDoorChanged berfungsi untuk mengganti fungsi dari Door dan DoorController.
``` C#
public DoorController(OnDoorChanged callbackOnDoorChanged)
        {
            this.callbackOnDoorChanged = callbackOnDoorChanged;
            this.door = new Door();
        }

        public void close()
        {
            this.door.close();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("CLOSED", "door closed");
        }
        public void open()
        {
            this.door.open();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("OPENED", "door opened");
        }
        public void activateLock()
        {
            this.door.activatelock();
            this.callbackOnDoorChanged.onDoorOpenStateChanged("LOCKED", "door locked");
        }
```


