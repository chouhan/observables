What is an observable?

It is like a publish subscribe. It simply is a DataSource. Examples are Events, Http Requests, etc..

It is a different type of approach used to handle asynchronous http requests.

Follows Observer pattern, which has Observable and Observer.

The data packages are emitted by Observable which can handle data, error and a success.

The observer (our code), which is like a subscribe function.

Note: Observable does not have to be completed

Example:

Subscriber/Receiver

ngOnInit() {
    this.route.params
      .subscribe(
        (params: Params) => {
          this.id = +params['id'];
        }
      );
  }


CREATING A OBSERVABLE AND A OBSERVER

const myObservable = Observable.create((observer: Observer<string>) => {
    setTimeout(() => {
        observer.next('first package'); // next() calls the next package.
    }, 1000);
    setTimeout(() => {
        observer.next('second package'); // next() calls the next package.
    }, 2000);
    setTimeout(() => {
        observer.error('This will not work'); // next() calls the next package.
    }, 3000);
    setTimeout(() => {
            //observer.error('This will not work'); // next() calls the next package.
            observer.complete();
        }, 4000);
    setTimeout(() => {
        observer.error('third package'); // next() calls the next package.
    }, 5000);
});

myObservable.subscribe(
    (data:string) => {console.log(data);}
    (error:string) => {console.log(error);}
    () => {console.log('completed')}
  );


UNSUBCRIBE TO OBSERVERABLE

To avoid memory leaks

subscription: Subscription;
ngOnDestroy() {
   this.subscription.unsubscribe(); 
}

USING SUBJECTS TO PASS AND LISTEN DATA

Subject basically is like an observable, but conviniently allows you to push new data during your code
Used for Cross Compoenent Communication. Similar to EventEmitters in Angular, where it is built on Subject.


