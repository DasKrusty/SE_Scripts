* Automated systems for AUHX-3 Sully

@variables {
    * Abreviated names for blocks
	PREA = "AUHX-3 Program [EAP]"
	LILA = "AUHX-3 Light Land"
	LIFL = "AUHX-3 Light Flood"
	LINA = "AUHX-3 Light Nav"
	LISE = "AUHX-3 Light Search"
	LISP = "AUHX-3 Light Spot"
	LITU = "AUHX-3 Light Turret"
	ECLA = "AUHX-3 Event Controller - Land"
	ECCO = "AUHX-3 Event Controller - Cockpit"
	LGHI = "AUHX-3 Hinge LG"
	LGPI = "AUHX-3 Piston LG"
	WEAT = "AUHX-3 Autocannon Turret"
	WECT = "AUHX-3 Custom Turret Controller"
	AIVE = "AUHX-3 Air Vent"
	GYRO = "AUHX-3 Gyroscope"
	BAHI = "AUHX-3 Hinge Bay"
	TISH = "AUHX-3 Timer Block - Shutdown"
	TIST = "AUHX-3 Timer Block - Start"
	ANTE = "AUHX-3 Antenna"
	LCDS = "AUHX-3 Holo LCD"
	OXTA = "AUHX-3 Oxygen Tank"
	HYHT = "AUHX-3 Hydrogen Tank"
	HYST = "AUHX-3 Hydrogen Thruster X"
	HYSS = "AUHX-3 Hydrogen Thruster S"
	HYLT = "AUHX-3 Large Hydrogen Thruster"
	LAGE = "AUHX-3 Landing Gear"
	BATT = "AUHX-3 Battery"
	COBE = "AUHX-3 Connector Below"
	CORE = "AUHX-3 Connector Rear"
	PARA = "AUHX-3 Parachute"
	BRCO = "AUHX-3 Broadcast Controller"
}

@Alt_Low {
	* Low Alt is triggered by an Event Controller when craft is below a set target
	Write to \PREA = "Low Altitude"
	OnOff_On \LILA
	OnOff_On \LIFL
	OnOff_Off \LINA
	OnOff_On \ECLA
	Rotate \LGHI to -45 at 5
	Move \LGPI to 0.8 at 1
}

@Alt_High {
	* Low Alt is triggered by an Event Controller when craft is below a set target
	Write to \PREA = "High Altitude"
	OnOff_Off \LILA
	OnOff_Off \LIFL
	OnOff_On \LINA
	OnOff_Off \ECLA
	Rotate \LGHI to -90 at 5
	Move \LGPI to 0 at 3
}

@Landed {
	Write to \PREA = "Landed"
	OnOff_On \ECCO
	OnOff_Off \WEAT
	Damp of MyShip = False
	Color of \LILA = 0:255:0
}

@Take_Off {
	Write to \PREA = "Lifted Off"
	OnOff_Off \ECCO
	OnOff_On \WEAT
	Damp of MyShip = True
	Color of \LILA = 255:255:255
}

@Cockpit_Out {
	Write to \PREA = "Exited Cockpit"
	OnOff_Off \AIVE
	OnOff_Off \GYRO
	Rotate \BAHI to -35 at 1
	Start \TISH
	Color of \LILA = 255:255:0
}

@Cockpit_In {
	Write to \PREA = "Entered Cockpit"
	OnOff_On \AIVE
	OnOff_On \GYRO
	Rotate \BAHI to 0 at 3
	Stop \TISH
	Start \TIST
	Color of \LILA = 0:255:0
}

@Timer_Shutdown {
	Write to \PREA = "Shutting Down"
	OnOff_Off \ANTE
	OnOff_Off \WECT
	OnOff_Off \LCDS
	Stockpile of \HYHT = True
	Stockpile of \OXTA = True
	OnOff_Off \HYST
	OnOff_Off \HYSS
	OnOff_Off \HYLT
	Lock \LAGE
	OnOff_Off \LISE
	OnOff_Off \LISP
	OnOff_Off \LITU
	OnOff_Off \LIFL
	Color of \LILA = 255:0:0
	If Status of AUHX-3 Connector Below = Connectable {
		Lock \COBE
		Transmit-Message-3 Broadcast Controller
		Color of \LILA = 0:0:255
		Recharge \BATT
	}
	If Status of AUHX-3 Connector Rear = Connectable {
		Lock \CORE
		Transmit-Message-3 Broadcast Controller
		Color of \LILA = 0:0:255
		Recharge \BATT
	}
	Delay 3000
	OnOff_Off \LILA
}

@Timer_Startup {
	Write to \PREA = "Starting Up"
	OnOff_On \ANTE
	OnOff_On \WECT
	OnOff_On \LCDS
	Stockpile of \HYHT = False
	Stockpile of \OXTA = False
	OnOff_On \HYST
	OnOff_On \HYLT
	Unlock \LAGE
	OnOff_On \LISP
	OnOff_On \LITU
	Discharge \BATT
	Unlock \CORE
	Unlock \COBE
	OnOff_On \LIFL
	OnOff_On \LILA
	Color of \LILA = 255:0:255
	if Planet Altitude of MyShip > 10000 {
		OnOff_On \HYSS
	}
}

@Space {
	if Color of AUHX-3 Light Land = 55:55:255 {
		OnOff_Off \HYSS
		Color of \LILA = 255:255:255
		Write to \PREA = "Space Travel Offline"
	}
	Else if Color of AUHX-3 Light Land = 255:255:255 {
		OnOff_On \HYSS
		Color of \LILA = 55:55:255
		Write to \PREA = "Space Travel Online"
	}
	Else if Color of AUHX-3 Light Land = 0:255:0 {
		Write to \PREA = "Take Off First"
	}
}

@Failure {
    OnOff_Off \HYLT
    OnOff_Off \HYST
	OnOff_Off \HYSS
    OnOff_Off \GYRO
    OnOff_On \BEAC
    Open_On \PARA
    Write to \PREA = "ASSISTANCE REQUIRED"
	Transmit-Message-1 Broadcast Controller
}

@Info {
    Write to \PREA = "EAP - V.1.78"
    WriteLine to \PREA = "Craft - V3.03"
}