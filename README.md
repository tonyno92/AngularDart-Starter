# AngularDart-Starter

## Requirements

To execute this project a Dart environment is required.

> flutterdev@fedora:~$ flutter --version

    **Flutter 3.7.12** • channel unknown • unknown source
    Framework • revision 4d9e56e694 (1 anno, 7 mesi fa) • 2023-04-17 21:47:46 -0400
    Engine • revision 1a65d409c7
    Tools • **Dart 2.19.6** • DevTools 2.20.1


## Execute

To execute this project go to root of your project and run this commands:

> flutterdev@fedora:~$ dart pub get
> 
> flutterdev@fedora:~$ dart pub global activate webdev
> 
> flutterdev@fedora:~$ dart pub global activate ngdart_cli
> 
> flutterdev@fedora:~$ webdev serve


## Knowed issues

### analyzer-4.7.0
  
if you encounter this issue, do this:
- Open this file with your prefered text editor
	> $ code ~/.pub-cache/hosted/pub.dev/analyzer-4.7.0/lib/src/dart/element/extensions.dart
- Replace the methos `Set<TargetKind> get targetKinds` with this body:
	> 
	    Set<TargetKind> get targetKinds {
	        final element = this.element;
	        InterfaceElement? interfaceElement;
	        if (element is PropertyAccessorElement) {
	          if (element.isGetter) {
	            var type = element.returnType;
	            if (type is InterfaceType) {
	              interfaceElement = type.element2;
	            }
	          }
	        } else if (element is ConstructorElement) {
	          interfaceElement = element.enclosingElement3;
	        }
	        if (interfaceElement == null) {
	          return const <TargetKind>{};
	        }
	        for (var annotation in interfaceElement.metadata) {
	          if (annotation.isTarget) {
	            var value = annotation.computeConstantValue()!;
	            var kinds = <TargetKind>{};
	            // REMOVED CODE WAS HERE
	            return kinds;
	          }
	        }
	        return const <TargetKind>{};
	      }

- Remove all previous build datas
	> flutterdev@fedora:**< root-project >**$ rm -rf .dart_tool


A web app that uses [AngularDart](https://angulardart.xyz) and
[AngularDart Components](https://pub.dev/ngcomponents).

Created from templates made available by Stagehand under a BSD-style
[license](https://github.com/dart-lang/stagehand/blob/master/LICENSE).
